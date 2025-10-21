# ☸️ AWS EKS (Elastic Kubernetes Service)

## 🌐 What is AWS EKS?
**Amazon Elastic Kubernetes Service (EKS)** is a **fully managed Kubernetes service** that allows you to **run Kubernetes clusters on AWS** without needing to install, operate, and maintain your own Kubernetes control plane.  

- It simplifies running **containerized applications** at scale.  
- EKS integrates with other AWS services like **IAM, VPC, CloudWatch, Fargate, ALB**, and more.  

> 💡 Think of EKS as **AWS’s managed Kubernetes service** — you manage applications, AWS manages the Kubernetes control plane.

---

## ⚙️ Key Features of AWS EKS
| Feature | Description |
|---------|-------------|
| **Managed Control Plane** | AWS handles provisioning, patching, scaling, and high availability of Kubernetes master nodes |
| **Worker Nodes** | EC2 instances or Fargate pods run container workloads |
| **Integration with AWS Services** | IAM, VPC, CloudWatch, ELB/ALB, Route 53, ECR |
| **Highly Available** | Control plane runs across multiple AZs with auto-recovery |
| **Security** | IAM roles, Security Groups, VPC isolation, and Secrets integration |
| **Auto Scaling** | Horizontal Pod Autoscaler (HPA) and Cluster Autoscaler supported |

---

## ⚙️ How AWS EKS Works
1. **Control Plane**: AWS manages Kubernetes master nodes (API server, etcd, scheduler).  
2. **Worker Nodes**: EC2 instances or Fargate run your containerized workloads.  
3. **Networking**: EKS runs within your VPC, supports private/public subnets, and integrates with **Security Groups**.  
4. **Storage**: EBS, EFS, or FSx can be used as persistent volumes.  
5. **Scaling**: Pods scale horizontally via HPA or cluster scales via Cluster Autoscaler.

```

[User App] -> [Pods] -> [Worker Nodes] -> [Control Plane Managed by AWS] -> [Networking & Storage]

````

---

## ⚙️ How to Configure AWS EKS

### Step 1️⃣ – Create IAM Role for EKS
- Go to **IAM Console → Roles → Create Role**  
- Service: **EKS**  
- Attach managed policies:
  - `AmazonEKSClusterPolicy`
  - `AmazonEKSServicePolicy`  
- Name: `EKS-ClusterRole`

### Step 2️⃣ – Create VPC for EKS
- AWS provides **default VPC template** for EKS with:
  - 2 public subnets (for load balancer)
  - 2 private subnets (for worker nodes)
  - Internet Gateway & NAT Gateway  
- Or use existing VPC.

### Step 3️⃣ – Create EKS Cluster
- Go to **EKS Console → Create Cluster**
- Configuration:
  - Name: `MyEKSCluster`
  - Kubernetes version: `1.28`
  - Cluster Service Role: `EKS-ClusterRole`
  - VPC & Subnets: Use prepared VPC
  - Security group: Allow API server access
- AWS provisions **Control Plane** (multi-AZ, highly available)
- Wait ~10–15 minutes for cluster creation

### Step 4️⃣ – Configure Worker Nodes (Node Group)
- Go to **Compute → Add Node Group**
- Configuration:
  - Node Role: `AmazonEKSWorkerNodeRole`
  - Node type: EC2 instance type (e.g., `t3.medium`)
  - Scaling: Min 1, Max 3, Desired 2 nodes
  - Subnets: Private or public subnets
- AWS provisions EC2 nodes and joins them to cluster automatically

### Step 5️⃣ – Configure `kubectl`
- Install **kubectl** and **aws-iam-authenticator** locally
- Update kubeconfig:
```bash
aws eks update-kubeconfig --region <region> --name MyEKSCluster
kubectl get nodes
````

* Output: Shows worker nodes connected to EKS cluster

---

## 🧩 Key Components of AWS EKS

| Component              | Description                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| **Control Plane**      | Managed Kubernetes masters (API server, etcd, scheduler)                  |
| **Worker Nodes**       | EC2 instances or Fargate pods running workloads                           |
| **Node Group**         | Set of EC2 instances in cluster for pod deployment                        |
| **Pod**                | Smallest deployable unit in Kubernetes (one or more containers)           |
| **Deployment**         | Controller for managing pod replicas and rollout updates                  |
| **Service**            | Exposes pods internally or externally (ClusterIP, LoadBalancer, NodePort) |
| **ConfigMap & Secret** | Store configuration and sensitive info                                    |
| **Persistent Volume**  | Attach EBS/EFS/FSx for storage to pods                                    |

---

## 💰 Pricing

* **EKS Control Plane**: ~$0.10 per hour per cluster (~$73/month)
* **Worker Nodes**: Pay for EC2 or Fargate resources running workloads
* **Storage**: EBS/EFS/FSx used by pods
* **Optional Services**: ALB, NAT Gateway, Data Transfer

> 💡 EKS itself charges only for the control plane; worker nodes are billed separately.

---

## 🧠 Practical Example: Deploy a Node.js App on EKS

### Scenario:

Deploy a **Node.js web application** on EKS using **Fargate profile** (serverless nodes).

---

### Step 1️⃣ – Create Node.js App and Docker Image

```javascript
// app.js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('☸️ Hello from AWS EKS!'));
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

* Build and push image to **Amazon ECR**

```bash
docker build -t eks-node-app .
docker tag eks-node-app:latest <account_id>.dkr.ecr.<region>.amazonaws.com/eks-node-app:latest
docker push <account_id>.dkr.ecr.<region>.amazonaws.com/eks-node-app:latest
```

---

### Step 2️⃣ – Create Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodejs-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nodejs-app
  template:
    metadata:
      labels:
        app: nodejs-app
    spec:
      containers:
      - name: nodejs
        image: <ECR IMAGE URL>
        ports:
        - containerPort: 8080
```

Apply deployment:

```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

---

### Step 3️⃣ – Expose Application via LoadBalancer

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nodejs-service
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: nodejs-app
```

Apply service:

```bash
kubectl apply -f service.yaml
kubectl get svc
```

* Wait a few minutes → LoadBalancer assigns a **public DNS**
* Open browser:
  `http://<LoadBalancer-DNS>` → Output: **☸️ Hello from AWS EKS!**

---

## ✅ Summary

| Feature                | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| **AWS EKS**            | Managed Kubernetes service                                   |
| **Control Plane**      | Managed by AWS, highly available                             |
| **Worker Nodes**       | EC2 or Fargate running pods                                  |
| **Node Groups**        | EC2 instances for container workloads                        |
| **Pods & Deployments** | Run containers and manage replicas                           |
| **Service**            | Expose apps internally or externally                         |
| **Storage**            | EBS, EFS, FSx persistent volumes                             |
| **Pricing**            | Pay for control plane + compute + storage                    |
| **Use Cases**          | Microservices, web apps, batch jobs, container orchestration |

---

### 💡 Tips for AWS EKS

1. Use **Fargate profile** for serverless nodes → reduces management overhead.
2. Enable **CloudWatch Container Insights** for monitoring CPU, memory, and network metrics.
3. Integrate with **ALB Ingress Controller** to route traffic to multiple services.
4. Use **Helm** to manage complex deployments easily.
5. Implement **IAM Roles for Service Accounts (IRSA)** for secure pod-level permissions.

---

This document provides a complete, end-to-end understanding of **AWS EKS**, including setup, deployment, scaling, monitoring, and practical container deployment.

---
