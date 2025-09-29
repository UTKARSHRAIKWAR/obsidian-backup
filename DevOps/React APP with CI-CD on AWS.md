# 🚀 Hosting React (Vite) App on AWS EC2 with Nginx + GitHub Actions (CI/CD)

## 1. Launch EC2 Instance
- Create an **Ubuntu** EC2 instance.
- Download the `.pem` key and SSH into your server:

```bash
chmod 400 aws.pem
ssh -i aws.pem ubuntu@<EC2_PUBLIC_IP>
```

- Update server:
```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install Nginx
```bash
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

Check:
```bash
curl http://localhost
```
✅ Should show **Welcome to nginx!**

---

## 3. Configure Security Group
- Open EC2 **Security Group** → **Inbound Rules**.
- Allow:
  - `22` (SSH)
  - `80` (HTTP)
  - `443` (HTTPS)

Now test `http://<EC2_PUBLIC_IP>` → should show Nginx page.

---

## 4. Deploy React (Vite) Build Manually (first time)
On your **local machine**:
	```bash
npm run build   # creates dist/ folder
```

Upload files to EC2:
```bash
scp -i aws.pem -r dist/* ubuntu@<EC2_PUBLIC_IP>:/var/www/html/
```

Reload Nginx:
```bash
sudo systemctl reload nginx
```

Now open `http://<EC2_PUBLIC_IP>` → should load React app.

---

## 5. Nginx Config for React SPA
Edit config:
```bash
sudo nano /etc/nginx/sites-available/react-app
```

Example:
```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

Enable & reload:
```bash
sudo ln -s /etc/nginx/sites-available/react-app /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## 6. Enable HTTPS (SSL)
Install Certbot:
```bash
sudo apt install certbot python3-certbot-nginx -y
```

Run:
```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

---

## 7. CI/CD with GitHub Actions
Inside your repo → `.github/workflows/deploy.yml`

```yaml
name: Deploy React to EC2

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: 📥 Checkout repo
        uses: actions/checkout@v4

      - name: ⚙️ Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "18"

      - name: 📦 Install dependencies
        run: npm ci

      - name: 🏗️ Build React app
        run: npm run build # Vite → dist/

      - name: 🔑 Prepare SSH key
        run: |
          echo "${{ secrets.EC2_SSH_KEY }}" > ./deploy_key
          chmod 600 ./deploy_key

      - name: 📡 Ensure rsync exists
        run: sudo apt-get update && sudo apt-get install -y rsync

      - name: 🚚 Deploy dist/ to EC2 via rsync
        env:
          SSH_PORT: 22
          EC2_USER: ${{ secrets.EC2_USER }}
          EC2_HOST: ${{ secrets.EC2_HOST }}
          DEPLOY_PATH: ${{ secrets.DEPLOY_PATH || '/var/www/html' }}
        run: |
          rsync -avz --delete -e "ssh -i ./deploy_key -o StrictHostKeyChecking=no -p $SSH_PORT" dist/ ${EC2_USER}@${EC2_HOST}:${DEPLOY_PATH}/

      - name: 🔄 Reload Nginx
        run: |
          ssh -i ./deploy_key -o StrictHostKeyChecking=no -p 22 ${{ secrets.EC2_USER }}@${{ secrets.EC2_HOST }} "sudo systemctl reload nginx"
```

---

## 8. Setup GitHub Secrets
In your repo → **Settings > Secrets and variables > Actions** → Add:
- `EC2_SSH_KEY` → contents of your `.pem`
- `EC2_USER` → `ubuntu`
- `EC2_HOST` → your EC2 Public IP or domain
- `DEPLOY_PATH` → `/var/www/html`

---

## 9. Workflow
1. Push code to `main` branch.
2. GitHub Actions:
   - Builds React app → `dist/`
   - Rsyncs to `/var/www/html`
   - Reloads Nginx
3. Your site auto-updates 🎉

---

# ✅ Summary
- Nginx serves static files from `/var/www/html`.
- GitHub Actions automates deployment with rsync.
- Certbot adds SSL for HTTPS.
- Every push to **main** → auto deploy to EC2.