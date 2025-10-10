
# 📁 File Storage Service Backend

A production-grade backend for a **File Storage System** built with **Node.js, Express, MongoDB, and AWS S3**.
Uses **Multer** for local temporary uploads and S3 for permanent cloud storage.

---

## 🧩 Overview
- Users can upload, download, list, and delete files.
- Files are temporarily stored locally, then uploaded to AWS S3.
- Generates **pre-signed URLs** for secure access.
- Stores metadata (name, size, key, owner, etc.) in MongoDB.

---

## ⚙️ Tech Stack
| Layer | Technology |
|-------|-------------|
| Backend | Node.js, Express |
| Database | MongoDB |
| Authentication | JWT |
| Storage | AWS S3 |
| Upload Middleware | Multer |
| Cloud SDK | AWS SDK v3 |
| Other Tools | dotenv, fs, bcrypt, jsonwebtoken |

---

## 📁 Project Structure
```
backend/
├── src/
│   ├── config/
│   │   └── s3.js
│   ├── controllers/
│   │   └── file.controller.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── upload.js
│   ├── models/
│   │   └── files.model.js
│   ├── routes/
│   │   └── file.routes.js
│   ├── utils/
│   │   └── logger.js
│   └── server.js
├── .env
├── package.json
└── README.md
```

---

## 🧠 Flow
1. User logs in → gets JWT token.
2. User uploads a file → multer saves locally.
3. File uploaded to AWS S3 via `PutObjectCommand`.
4. Local file deleted.
5. Metadata stored in MongoDB.
6. Generate **signed URL** for secure download.

---

## 🪣 AWS S3 Setup
1. Create a bucket in S3.
2. Create IAM user → assign permissions:
   - `s3:PutObject`
   - `s3:GetObject`
   - `s3:DeleteObject`
3. Add keys to `.env`:
   ```
   AWS_BUCKET_NAME=my-bucket
   AWS_ACCESS_KEY_ID=xxxx
   AWS_SECRET_ACCESS_KEY=xxxx
   AWS_REGION=ap-south-1
   ```
4. Enable **Block Public Access** for safety.

---

## 🧰 Multer Setup
- Multer saves temporary files to `/uploads`.
- Once uploaded to S3 → file deleted from local.
```js
import multer from "multer";

const storage = multer.diskStorage({
  destination: "uploads/",
  filename: (req, file, cb) => cb(null, Date.now() + "-" + file.originalname)
});

export default multer({ storage });
```

---

## 📦 API Endpoints
| Method | Route | Description | Auth |
|--------|--------|--------------|------|
| `POST` | `/api/upload` | Upload file to S3 | ✅ |
| `GET` | `/api/files` | List user files | ✅ |
| `GET` | `/api/files/:id` | Get file (signed URL) | ✅ |
| `DELETE` | `/api/files/:id` | Delete file | ✅ |

---

## 🧾 Example Response
```json
{
  "success": true,
  "file": {
    "_id": "652d23f3b4d9a2",
    "fileName": "resume.pdf",
    "url": "https://s3.amazonaws.com/...",
    "size": 12345
  }
}
```

---

## 🔒 Security Best Practices
- Never expose AWS credentials.
- Use **signed URLs** instead of public links.
- Validate file types and size.
- Clean up local temp files.
- Use HTTPS in production.
- Configure S3 CORS properly.

---

## 🚀 Deployment Notes
- Use **PM2** or **Docker** for backend.
- Use **Nginx** as reverse proxy.
- Configure **ENV variables** securely.
- Add **rate limiting** and **helmet** for protection.

---

## 🧩 Future Enhancements
- File sharing via short links.
- Folder management.
- File preview support.
- Expiry for signed URLs.
- Storage analytics dashboard.

---

## 📘 Author
**Utkarsh Raikwar**  
Full Stack Developer | Cloud Enthusiast  
GitHub: [github.com/utkarshraikwar](https://github.com/utkarshraikwar)