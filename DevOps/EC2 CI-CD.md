# 🚀 Deploy React App to AWS EC2 using GitHub Actions

This document explains a **CI/CD workflow** for automatically **building** and **deploying a React app** to an **EC2 server** whenever changes are pushed to the `main` branch.  

---

## ⚡ Workflow Overview
- 🟢 Triggered when code is pushed to **`main` branch**  
- ⚙️ Runs on **Ubuntu GitHub Actions runner**  
- 📦 Installs dependencies and **builds React app**  
- 🔑 Uses SSH to securely connect to **EC2 instance**  
- 📤 Deploys the built app to **`/var/www/html`** (or a custom path)  
- 🌐 Reloads **Nginx** to serve the latest version  

---

## 🛠️ Workflow File (`.github/workflows/deploy.yml`)

```yaml
name: Deploy React to EC2

on:
  push:
    branches: [main] # 🚀 Deploy on pushes to main branch

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
        run: npm run build   # ⚠️ Default output is 'build/', not 'dist/'

      - name: 🔑 Prepare SSH key
        run: |
          echo "${{ secrets.EC2_SSH_KEY }}" > ./deploy_key
          chmod 600 ./deploy_key

      - name: 📡 Ensure rsync exists
        run: sudo apt-get update && sudo apt-get install -y rsync

      - name: 🚚 Deploy build/ to EC2 via rsync
        env:
          SSH_PORT: 22
          EC2_USER: ${{ secrets.EC2_USER }}
          EC2_HOST: ${{ secrets.EC2_HOST }}
          DEPLOY_PATH: ${{ secrets.DEPLOY_PATH || '/var/www/html' }}
        run: |
          rsync -avz --delete -e "ssh -i ./deploy_key -o StrictHostKeyChecking=no -p $SSH_PORT" build/ ${EC2_USER}@${EC2_HOST}:${DEPLOY_PATH}/

      - name: 🔄 Reload Nginx
        run: |
          ssh -i ./deploy_key -o StrictHostKeyChecking=no -p 22 ${{ secrets.EC2_USER }}@${{ secrets.EC2_HOST }} "sudo systemctl reload nginx"
```

---

## 🧩 Step-by-Step Explanation

### 1. 📥 Checkout Repo
Pulls your repository into the GitHub Actions runner.

### 2. ⚙️ Setup Node.js
Installs **Node.js v18** so you can build and run your React app.

### 3. 📦 Install Dependencies
Runs `npm ci` → installs exact dependencies from `package-lock.json`.

### 4. 🏗️ Build React App
Runs `npm run build` → generates optimized static files inside `build/`.

### 5. 🔑 Prepare SSH Key
- Reads private key from secret `EC2_SSH_KEY`  
- Saves it as `deploy_key` with proper permissions.

### 6. 📡 Ensure rsync Exists
Installs `rsync` so files can be copied to EC2.

### 7. 🚚 Deploy to EC2
Uses `rsync` over SSH to transfer the `build/` folder to your server.  
- `--delete` removes old unused files  
- `-avz` ensures fast, compressed, incremental updates  
- Target: `${DEPLOY_PATH}` (default `/var/www/html`)  

### 8. 🔄 Reload Nginx
SSH into the server and reloads **Nginx** so the new build is served immediately.

---

## 🔐 Required GitHub Secrets

| Secret Name   | 📝 Description |
|---------------|----------------|
| `EC2_SSH_KEY` | Your private SSH key (matches public key in EC2) |
| `EC2_USER`    | EC2 username (e.g., `ubuntu`, `ec2-user`) |
| `EC2_HOST`    | Public IP or domain of your EC2 instance |
| `DEPLOY_PATH` | (Optional) Directory to deploy React build (default: `/var/www/html`) |

---

## ⚠️ Important Notes
- 🛑 Default React build output = **`build/`**, not `dist/`. Ensure workflow matches your setup.  
- 🔒 SSH key must already be added to **`~/.ssh/authorized_keys`** on EC2.  
- 🌍 EC2 security group must allow **SSH (22)** and **HTTP/HTTPS (80/443)**.  

---

## ✅ Summary
With this setup:
1. Push to `main` → workflow runs automatically.  
2. React app is built and deployed to EC2.  
3. Nginx reloads → your website serves the latest code instantly 🎉.  

---

✨ Now you have **continuous deployment** for your React app straight to AWS EC2!