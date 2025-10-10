# Cloud Infrastructure Management Dashboard

## 🚀 Overview
The **Cloud Infrastructure Management Dashboard** is a backend project designed to provide users with a web-based interface to manage AWS resources — EC2, S3, and Lambda — through secure backend APIs. It mimics core AWS Console functionalities on a smaller scale.

---

## 🧱 Tech Stack

| Layer                   | Tech                              |
| ----------------------- | --------------------------------- |
| **Frontend (Optional)** | Next.js, TailwindCSS, Chart.js    |
| **Backend**             | Node.js + Express.js              |
| **Database**            | MongoDB                           |
| **Cloud SDK**           | AWS SDK for JavaScript (v3)       |
| **Auth**                | AWS IAM OAuth / Custom JWT System |
| **Optional**            | Redis (cache), BullMQ (jobs)      |

---

## ⚙️ Features

### 1. AWS Authentication
- Secure IAM key storage using encryption (AWS KMS or crypto-js)
- OAuth-style integration for user credentials
- Temporary credentials with AWS STS

### 2. Resource Management APIs

#### 🖥 EC2 Management
- `GET /api/ec2/instances` → List all EC2 instances
- `POST /api/ec2/start/:id` → Start instance
- `POST /api/ec2/stop/:id` → Stop instance
- `DELETE /api/ec2/terminate/:id` → Terminate instance

#### 📦 S3 Management
- `GET /api/s3/buckets` → List buckets
- `POST /api/s3/create` → Create bucket
- `POST /api/s3/upload` → Upload file
- `DELETE /api/s3/:name` → Delete bucket

#### ⚙️ Lambda Management
- `GET /api/lambda/functions` → List functions
- `POST /api/lambda/invoke/:name` → Invoke function
- `POST /api/lambda/deploy` → Deploy function

### 3. Usage Analytics & Cost Tracking
- AWS Cost Explorer API integration
- Resource usage stats (EC2 uptime, S3 storage size)
- MongoDB analytics snapshots
- Charts using Chart.js or Recharts

### 4. Logging & Monitoring
- Track API calls (user, operation, resource, timestamp)
- Store logs in MongoDB

### 5. Dashboard UI (Optional)
- Built with Next.js + TailwindCSS
- Pages: `/dashboard`, `/ec2`, `/s3`, `/lambda`, `/analytics`
- Real-time updates via WebSockets

---

## 🔒 Security
- Encrypt stored credentials
- Use IAM policies with least privilege
- JWT auth and rate limiting for your API

---

## 🧠 Bonus Features
- Role-based access (Admin/Viewer)
- Auto-scaling (start EC2 on high CPU)
- Cost threshold notifications
- Multi-account AWS management
- Themed analytics dashboard

---

## 📁 Folder Structure
```
cloud-dashboard/
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── routes/
│   │   ├── models/
│   │   ├── utils/
│   │   └── app.js
│   └── package.json
└── frontend/
    ├── pages/
    ├── components/
    └── package.json
```

---

## 💡 Example AWS Client Setup
```js
// utils/awsClient.js
import { EC2Client } from "@aws-sdk/client-ec2";

export const getEC2Client = (accessKey, secretKey, region = "us-east-1") =>
  new EC2Client({
    region,
    credentials: { accessKeyId: accessKey, secretAccessKey: secretKey },
  });
```

---

## 📊 Example API Design (EC2)
```js
import { DescribeInstancesCommand } from "@aws-sdk/client-ec2";
import { getEC2Client } from "../utils/awsClient.js";

export const listInstances = async (req, res) => {
  const { accessKey, secretKey, region } = req.user.awsCredentials;
  const ec2 = getEC2Client(accessKey, secretKey, region);
  const command = new DescribeInstancesCommand({});
  const response = await ec2.send(command);
  res.json(response.Reservations);
};
```

---

## ✅ Outcome
- Demonstrates advanced backend engineering skills.
- Highlights cloud integration experience with AWS.
- Perfect for showcasing secure API design, DevOps familiarity, and dashboard analytics.