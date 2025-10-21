# 🌿 AWS Elastic Beanstalk

## 🌐 What is AWS Elastic Beanstalk?
**AWS Elastic Beanstalk** is a **Platform as a Service (PaaS)** that helps developers quickly deploy, manage, and scale web applications and services without worrying about the underlying infrastructure.  
You simply upload your code, and Beanstalk automatically handles:
- Provisioning EC2 instances  
- Load balancing & scaling  
- Health monitoring  
- Environment management  

> 💡 Think of it as “EC2 + Load Balancer + Auto Scaling + CloudWatch” all bundled together and managed for you.

---

## ⚙️ How to Configure Elastic Beanstalk

1. **Open AWS Console** → Navigate to **Elastic Beanstalk**.
2. Click **Create Application**.
3. Enter:
   - **Application Name** → e.g., `MyWebApp`
   - **Platform** → e.g., `Python`, `Node.js`, `Java`, or `Docker`
4. Upload your **application code** (ZIP file or GitHub link).
5. Choose **Environment Type**:
   - Web Server Environment (for web apps)
   - Worker Environment (for background jobs)
6. Configure Environment:
   - Instance type (e.g., `t3.micro`)
   - VPC, subnets, and key pairs
   - Scaling options (min/max instances)
7. Review and **Launch Application**.

Beanstalk will:
- Create EC2 instances
- Set up Auto Scaling, ELB, CloudWatch, and S3 bucket
- Deploy your app automatically 🎉

---

## 🌱 Types of Environments

| Type | Description |
|------|--------------|
| **Web Server Environment** | Handles HTTP/S requests via Elastic Load Balancer (e.g., websites, APIs) |
| **Worker Environment** | Processes background jobs using SQS (e.g., sending emails, processing logs) |

---

## 🧩 Platforms Supported
Elastic Beanstalk supports multiple programming platforms:

| Category | Examples |
|-----------|-----------|
| **Languages** | Java, Python, PHP, Node.js, Ruby, Go, .NET |
| **Web Servers** | Apache, Nginx, Passenger, IIS |
| **Containers** | Docker, Tomcat |
| **Custom Platform** | Bring your own environment configuration |

> You can also create a **custom platform** using **Packer** if your runtime isn’t listed.

---

## 🚀 Deployment Models in Elastic Beanstalk

| Model | Description | Use Case |
|--------|--------------|----------|
| **All at Once** | Deploys new version to all instances simultaneously | Fast, but downtime possible |
| **Rolling** | Updates instances in batches | Reduces downtime |
| **Rolling with Additional Batch** | Launches new batch before terminating old ones | Ensures capacity |
| **Immutable** | Launches new instances with new version, swaps after success | Safest deployment |
| **Blue/Green Deployment** | Creates new environment (Green), then swaps traffic from old one (Blue) | Zero downtime deployment |

---

## ⚖️ Traffic Splitting (Canary Deployment)
Elastic Beanstalk supports **Traffic Splitting** which gradually shifts a percentage of user traffic to the new version.  
- Example: 10% traffic to new version for testing → then 100% if healthy.  
- Ideal for **canary testing** and safe rollouts.

---

## 💰 Pricing
Elastic Beanstalk itself is **free**, but you pay for the AWS resources it provisions:
- **EC2 instances**
- **Elastic Load Balancer**
- **Auto Scaling**
- **S3 storage**
- **CloudWatch metrics**

> Example: A simple app using 1 `t3.micro` EC2 + ELB may cost only a few dollars/month.

---

## 🧠 Practical Example: Deploying a Node.js Web App

### Goal:
Deploy a Node.js website on AWS with zero manual server setup.

### Steps:
1. **Create a folder and app**
   ```bash
   mkdir my-node-app && cd my-node-app
   npm init -y
   npm install express
   
2. **Add `app.js`**

   ```javascript
   const express = require('express');
   const app = express();
   app.get('/', (req, res) => res.send('🌿 Hello from Elastic Beanstalk!'));
   app.listen(8080, () => console.log('Server running on port 8080'));
   ```
3. **Create `package.json` and zip the files**

   ```bash
   zip -r myapp.zip .
   ```
4. **Upload to Beanstalk**

   * AWS Console → Elastic Beanstalk → Create Application
   * Platform: Node.js
   * Upload: `myapp.zip`
5. **Launch**

   * Beanstalk provisions EC2, ELB, Auto Scaling, etc.
6. **Access the app**

   * Open Beanstalk URL:
     `http://my-node-app-env.elasticbeanstalk.com`

🎉 You’ll see your running Node.js web app!

---

## ✅ Summary

| Component               | Description                                      |
| ----------------------- | ------------------------------------------------ |
| **Elastic Beanstalk**   | PaaS for auto-managed app deployment             |
| **Environment Types**   | Web Server, Worker                               |
| **Platforms Supported** | Java, Node.js, Python, Docker, etc.              |
| **Deployment Models**   | Rolling, Immutable, Blue/Green                   |
| **Traffic Splitting**   | Canary testing for safer rollout                 |
| **Pricing**             | Pay only for underlying AWS resources            |
| **Use Case**            | Deploy apps fast without managing infrastructure |

---

### 💡 Tip:

Integrate Elastic Beanstalk with **AWS CodePipeline** for full CI/CD automation — from Git commit to live deployment.

```
