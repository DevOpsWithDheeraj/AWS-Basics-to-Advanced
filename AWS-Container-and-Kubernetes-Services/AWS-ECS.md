# 🐳 AWS ECS (Elastic Container Service)

## 🌐 What is AWS ECS?
**Amazon ECS (Elastic Container Service)** is a **fully managed container orchestration service** that allows you to run, manage, and scale **Docker containers** on AWS.  

- Supports **EC2 launch type** (you manage EC2 instances) and **Fargate launch type** (serverless, no EC2 management).  
- Ideal for microservices, APIs, batch jobs, and web applications.

> 💡 Think of ECS as AWS’s own Kubernetes-like container orchestration service.

---

## ⚙️ How AWS ECS Works
1. **Create a Cluster** → Logical group of resources (EC2 instances or Fargate)  
2. **Define Task Definition** → Blueprint specifying:
   - Docker image
   - CPU & memory
   - Ports & environment variables
   - IAM role
3. **Create a Service** → Defines how many tasks to run and maintain  
4. **Deploy Tasks** → ECS scheduler launches containers based on task definition  
5. **Scaling** → Auto-scaling based on CPU, memory, or custom metrics  

---

## ⚙️ How to Configure AWS ECS

### Step 1️⃣ – Create an ECS Cluster
1. Go to **ECS Console → Clusters → Create Cluster**  
2. Choose:
   - **EC2 Linux + Networking** → you manage EC2 instances  
   - **Networking only (Fargate)** → serverless option  
3. Name: `MyECSCluster`  
4. Configure:
   - VPC and subnets  
   - EC2 instance type (for EC2 launch)  
   - Number of instances  

---

### Step 2️⃣ – Create Task Definition
- Go to **Task Definitions → Create New Task Definition**  
- Choose launch type: EC2 or Fargate  
- Configure:
  - Container name  
  - Docker image (ECR or Docker Hub)  
  - CPU, memory  
  - Port mappings (e.g., 80 → 8080)  
  - Environment variables  
  - IAM role for the task  

---

### Step 3️⃣ – Create ECS Service
- Go to **Services → Create**  
- Choose:
  - Cluster: `MyECSCluster`  
  - Launch type: EC2 or Fargate  
  - Task definition: `MyTaskDefinition`  
  - Number of tasks (desired count)  
- Configure **load balancer** (optional)  
- Click **Create Service** → ECS scheduler launches tasks

---

### Step 4️⃣ – Deploy & Monitor
- ECS runs tasks on cluster instances  
- Monitor via:
  - CloudWatch metrics (CPU, memory)  
  - ECS Console (tasks, events, logs)  

---

## 🧩 Key Components of ECS

| Component | Description |
|-----------|-------------|
| **Cluster** | Logical grouping of resources (EC2/Fargate) |
| **Task Definition** | Blueprint of container configuration |
| **Task** | Running instance of a task definition |
| **Service** | Maintains desired task count and auto-replaces failed tasks |
| **Container Agent** | Runs on EC2 instances to manage containers |
| **Registry** | Stores container images (ECR or Docker Hub) |

---

## 💰 Pricing
- ECS itself **has no additional cost**  
- Pay for underlying resources:
  - EC2 instances (EC2 launch type)  
  - vCPU/memory (Fargate launch type)  
  - EBS volumes  
- Optional: Elastic Load Balancer, CloudWatch Logs

---

## 🧠 Practical Example: Deploy Node.js App on ECS Fargate

### Scenario:
Deploy a simple **Node.js web application** using ECS + Fargate.

---

### Step 1️⃣ – Containerize the App
```javascript
// app.js
const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('🐳 Hello from ECS Fargate!'));
app.listen(8080, () => console.log('Server running on port 8080'));
````

**Dockerfile**

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "app.js"]
EXPOSE 8080
```

* Build and push Docker image to **Amazon ECR**:

```bash
aws ecr create-repository --repository-name ecs-node-app
docker build -t ecs-node-app .
docker tag ecs-node-app:latest <account_id>.dkr.ecr.<region>.amazonaws.com/ecs-node-app:latest
docker push <account_id>.dkr.ecr.<region>.amazonaws.com/ecs-node-app:latest
```

---

### Step 2️⃣ – Create ECS Cluster

* Cluster type: **Networking only (Fargate)**
* Name: `NodeAppCluster`

---

### Step 3️⃣ – Create Task Definition

* Launch type: **Fargate**
* Container name: `NodeApp`
* Image: `<ECR URL>`
* CPU: 0.25 vCPU
* Memory: 512 MB
* Port mapping: 8080

---

### Step 4️⃣ – Create ECS Service

* Cluster: `NodeAppCluster`
* Launch type: **Fargate**
* Number of tasks: 1
* Configure public subnets and security group (allow port 8080)

---

### Step 5️⃣ – Access the App

* ECS launches the task via Fargate
* Find **Public IP** from task → open in browser:
  `http://<public-ip>:8080`
* Output: **🐳 Hello from ECS Fargate!**

---

## ✅ Summary

| Feature             | Description                                         |
| ------------------- | --------------------------------------------------- |
| **ECS**             | Managed container orchestration service             |
| **Launch Types**    | EC2 (self-managed) or Fargate (serverless)          |
| **Cluster**         | Logical grouping of resources                       |
| **Task Definition** | Container blueprint                                 |
| **Service**         | Maintains running tasks                             |
| **Pricing**         | Pay for EC2/Fargate, storage, and optional services |
| **Best Use Cases**  | Microservices, APIs, batch jobs, containerized apps |

---

### 💡 Tip:

Combine **ECS + Fargate + ALB + CloudWatch** to create a **fully managed, auto-scaling containerized application** without managing EC2 instances.

---
