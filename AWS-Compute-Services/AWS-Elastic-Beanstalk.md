# 🌿 AWS Elastic Beanstalk
---

## 🌱 What is AWS Elastic Beanstalk?

**AWS Elastic Beanstalk** is a **Platform-as-a-Service (PaaS)** that helps you **deploy, manage, and scale web applications** automatically — without worrying about the underlying infrastructure (like EC2, Load Balancer, or Auto Scaling).

👉 You just upload your application code (Java, Python, Node.js, PHP, etc.), and Elastic Beanstalk automatically handles:

* EC2 provisioning
* Load Balancing
* Auto Scaling
* Monitoring via CloudWatch

You can focus on **code**, not servers.

---

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

## 🔹 Key Concepts in Elastic Beanstalk

| Concept                       | Explanation                                                                                                                                                                              | Example                                                                                                            |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Application**               | A **logical container** for all related Elastic Beanstalk components (versions, environments, configurations).                                                                           | Suppose you create an app called **“MyWebApp”** — it may contain multiple environments like *dev*, *test*, *prod*. |
| **Application Version**       | A **specific, deployable version** of your application code (a ZIP or WAR file uploaded to S3).                                                                                          | Version 1.0 of “MyWebApp” might contain code uploaded on Oct 1, and Version 2.0 on Oct 10.                         |
| **Environment**               | An **instance of your application** running on AWS. Each environment runs one application version.                                                                                       | “MyWebApp-prod” might be one environment, and “MyWebApp-dev” another.                                              |
| **Environment Tier**          | Determines the **type of workload** the environment runs:  <br>• **Web Server tier** – handles HTTP requests (e.g., web apps). <br>• **Worker tier** – handles background jobs from SQS. | Web Tier → Node.js website; Worker Tier → background image processing queue.                                       |
| **Environment Configuration** | The **set of settings** defining how your environment runs — instance type, scaling, VPC, database, etc.                                                                                 | You might set EC2 type = t3.medium, Auto Scaling = min 2 max 4, DB = RDS MySQL.                                    |
| **Saved Configuration**       | A **snapshot** of environment settings that can be reused later to create or restore environments.                                                                                       | You can save “ProdConfig-v1” and apply it to new environments for testing or cloning.                              |
| **Platform**                  | The **software stack** Elastic Beanstalk uses — includes OS, runtime, and web server.                                                                                                    | Example: *64bit Amazon Linux 2 running Python 3.9* or *Node.js 18 on AL2023*.                                      |

---

## ⚙️ How It Works — Step-by-Step Example

Let’s say you have a **Python web app**.

1. **Create Application** → Name it `MyWebApp`.
2. **Upload Application Version** → Upload a ZIP file of your app (`mywebapp-v1.zip`) → stored in S3.
3. **Create Environment** → Choose “Web Server Environment” tier → Beanstalk launches EC2, Load Balancer, Auto Scaling, and deploys your app.
4. **Monitor & Update** → You can check logs, health metrics, and if you upload a new version (`mywebapp-v2.zip`), Beanstalk can deploy it with zero downtime (rolling updates).
5. **Save Configuration** → If your configuration works well, save it as `MyWebApp-Prod-Config`.
6. **Reuse Platform** → You might choose “Python 3.9 on AL2” as your platform for consistency across all environments.

---

## 🧩 Example Visualization

```
Application: MyWebApp
│
├── Application Versions:
│   ├── v1 (initial release)
│   └── v2 (bug fix)
│
├── Environments:
│   ├── MyWebApp-Dev (Web Tier, using v1)
│   └── MyWebApp-Prod (Web Tier, using v2)
│
├── Environment Configurations:
│   ├── Dev: 1 t3.micro instance
│   └── Prod: Auto Scaling (2–5 instances)
│
├── Saved Configurations:
│   └── ProdConfig-v1
│
└── Platform:
    └── 64bit Amazon Linux 2 running Python 3.9
```

---

## ✅ Summary

| Term                      | Description                                   | Example            |
| ------------------------- | --------------------------------------------- | ------------------ |
| Application               | Logical container for versions & environments | `MyWebApp`         |
| Application Version       | Uploaded code (ZIP/WAR) stored in S3          | `v1`, `v2`         |
| Environment               | Running version of your app                   | `MyWebApp-Prod`    |
| Environment Tier          | Web Server / Worker                           | Web tier = website |
| Environment Configuration | Environment’s settings                        | EC2 type, scaling  |
| Saved Configuration       | Reusable snapshot of settings                 | `ProdConfig-v1`    |
| Platform                  | OS + runtime + web server                     | Python 3.9 on AL2  |

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

---
