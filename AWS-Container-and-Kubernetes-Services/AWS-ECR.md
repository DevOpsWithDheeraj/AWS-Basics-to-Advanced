# 🖼️ AWS ECR (Elastic Container Registry)

## 🌐 What is AWS ECR?
**Amazon Elastic Container Registry (ECR)** is a **fully managed Docker container registry** that makes it easy to **store, manage, and deploy container images** for use with **Amazon ECS, EKS, and Fargate**.  

- Eliminates the need to operate your own container repository.  
- Integrated with **IAM** for fine-grained access control and **AWS CloudTrail** for auditing.  
- Fully compatible with Docker CLI, so developers can push and pull images seamlessly.

> 💡 Think of AWS ECR as **AWS’s version of Docker Hub** but private, secure, and highly available.

---

## ⚙️ Key Features of AWS ECR
| Feature | Description |
|---------|-------------|
| **Managed Registry** | AWS handles infrastructure, scaling, patching, and availability |
| **Private Repositories** | Store private Docker images with controlled access |
| **Public Repositories** | Optional public repositories for sharing images publicly |
| **Secure** | Integrated with IAM, KMS encryption, and TLS for data in transit |
| **High Availability** | Multi-AZ architecture ensures durability and reliability |
| **Integration** | Works seamlessly with ECS, EKS, Fargate, and CI/CD pipelines |
| **Vulnerability Scanning** | Built-in image scanning for security compliance |
| **Lifecycle Policies** | Automatically remove old or unused images |

---

## ⚙️ How AWS ECR Works
1. **Create a Repository** → Private or public container repository.  
2. **Push Images** → Use Docker CLI to build and push container images.  
3. **Pull Images** → Use ECS, EKS, or local Docker environment to pull images.  
4. **Manage Versions** → Tag images for version control and CI/CD deployment.  
5. **Secure Access** → Use IAM policies and roles to control who can push or pull images.

---

## ⚙️ How to Configure AWS ECR

### Step 1️⃣ – Create an ECR Repository
1. Go to **AWS ECR Console → Repositories → Create repository**  
2. Choose:
   - Repository name: `my-app-repo`  
   - Visibility: Private (default) or Public  
   - Encryption: AWS-managed KMS (default)  
   - Scan on push: Enabled (recommended)
3. Click **Create repository**  

---

### Step 2️⃣ – Authenticate Docker with ECR
```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
````

---

### Step 3️⃣ – Build and Tag Docker Image

```bash
docker build -t my-app .
docker tag my-app:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app-repo:latest
```

---

### Step 4️⃣ – Push Docker Image to ECR

```bash
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app-repo:latest
```

---

### Step 5️⃣ – Pull Docker Image from ECR

```bash
docker pull <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app-repo:latest
```

---

## 🧩 Integration with AWS Services

| Service                      | Use Case                                                 |
| ---------------------------- | -------------------------------------------------------- |
| **ECS**                      | Run containerized apps using images from ECR             |
| **EKS**                      | Deploy Kubernetes pods using ECR images                  |
| **Fargate**                  | Run serverless container workloads using images from ECR |
| **CodeBuild / CodePipeline** | Continuous integration and deployment workflows          |
| **CloudWatch**               | Monitor repository events and image push/pull logs       |

---

## 💰 Pricing

* **Storage**: $0.10 per GB per month (for private repositories)
* **Data Transfer**: Standard AWS data transfer rates for pulling/pushing images
* **Public Repositories**: Free for first 500 GB storage and 500 GB data transfer per month
* **Lifecycle Policies**: Free

> AWS ECR is cost-effective because you pay only for what you use, and it scales automatically.

---

## 🧠 Practical Example: Deploy Node.js App Using AWS ECR + ECS

### Step 1️⃣ – Containerize the Node.js App

```javascript
// app.js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('🖼️ Hello from AWS ECR!'));
app.listen(8080, () => console.log('Server running on port 8080'));
```

**Dockerfile**

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD ["node", "app.js"]
```

---

### Step 2️⃣ – Create ECR Repository

```bash
aws ecr create-repository --repository-name my-app-repo
```

---

### Step 3️⃣ – Authenticate Docker with ECR

```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
```

---

### Step 4️⃣ – Build, Tag, and Push Image

```bash
docker build -t my-app .
docker tag my-app:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app-repo:latest
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app-repo:latest
```

---

### Step 5️⃣ – Deploy on ECS

1. Create **ECS Cluster** (Fargate or EC2 launch type)
2. Create **Task Definition**:

   * Container image: `<ECR IMAGE URL>`
   * CPU & Memory
   * Port: 8080
3. Create **ECS Service**:

   * Launch type: Fargate
   * Desired tasks: 1–2
   * Public subnets and security group allowing port 8080

* Access the app via public IP / load balancer:
  `http://<public-ip>:8080` → Output: **🖼️ Hello from AWS ECR!**

---

## ✅ Summary

| Feature          | Description                                                    |
| ---------------- | -------------------------------------------------------------- |
| **AWS ECR**      | Fully managed Docker container registry                        |
| **Repositories** | Private or public storage for container images                 |
| **Integration**  | ECS, EKS, Fargate, CI/CD pipelines                             |
| **Security**     | IAM roles, KMS encryption, TLS, vulnerability scanning         |
| **Pricing**      | Pay per storage and data transfer                              |
| **Use Cases**    | Store container images for web apps, microservices, batch jobs |

---

### 💡 Tips for AWS ECR

1. Enable **Scan on Push** to automatically detect vulnerabilities in container images.
2. Use **Lifecycle Policies** to remove old or unused images automatically.
3. Integrate with **CodePipeline + CodeBuild** for CI/CD automation.
4. Use IAM roles with least privilege for secure repository access.
5. Prefer **private repositories** for production workloads; public repos for open-source sharing.

---
