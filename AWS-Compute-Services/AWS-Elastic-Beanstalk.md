# 🌿 AWS Elastic Beanstalk
---

## 🌱 1. What is AWS Elastic Beanstalk?

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

## ⚙️ 2. How to Configure Elastic Beanstalk

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

## 🌱 3. Types of Environments

| Type | Description |
|------|--------------|
| **Web Server Environment** | Handles HTTP/S requests via Elastic Load Balancer (e.g., websites, APIs) |
| **Worker Environment** | Processes background jobs using SQS (e.g., sending emails, processing logs) |

---

## 🧩 4. Platforms Supported
Elastic Beanstalk supports multiple programming platforms:

| Category | Examples |
|-----------|-----------|
| **Languages** | Java, Python, PHP, Node.js, Ruby, Go, .NET |
| **Web Servers** | Apache, Nginx, Passenger, IIS |
| **Containers** | Docker, Tomcat |
| **Custom Platform** | Bring your own environment configuration |

> You can also create a **custom platform** using **Packer** if your runtime isn’t listed.

---

## 🚀 5. AWS Elastic Beanstalk Deployment Models (Policies)

| **Deployment Model**              | **How It Works**                                                                                                                 | **Downtime**                  | **Rollback**                                    | **Cost Impact**                             | **Best Use Case**                                   | **Notes / Behavior**                            |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- | ----------------------------------------------- | ------------------------------------------- | --------------------------------------------------- | ----------------------------------------------- |
| **All at Once**                   | Deploys new version to **all instances simultaneously**.                                                                         | ⚠️ Possible (short downtime). | ❌ Manual rollback needed.                       | 💲 Low (no extra instances).                | Dev/Test environments.                              | Fastest, but risky for production.              |
| **Rolling**                       | Deploys new version to a **subset (batch)** of instances, replaces old ones gradually.                                           | ✅ No downtime (if healthy).   | ❌ Manual rollback required.                     | 💲 Normal (uses existing instances).        | Production environments with moderate traffic.      | Keeps capacity slightly reduced during update.  |
| **Rolling with Additional Batch** | Creates **temporary instances** for each batch to maintain full capacity while deploying.                                        | ✅ No downtime.                | ❌ Manual rollback.                              | 💲💲 Slightly higher (temporary resources). | Production systems needing continuous availability. | Ensures full capacity during deployment.        |
| **Immutable**                     | Deploys new version to a **completely new set of instances**, shifts traffic when healthy.                                       | ✅ No downtime.                | ✅ Easy rollback (just terminate new instances). | 💲💲 Higher (temporary full environment).   | Critical production systems.                        | Safest method before traffic splitting existed. |
| **Traffic Splitting (Canary)**    | Temporarily launches new instances and routes a **small % of traffic** to test new version. If successful → shifts 100% traffic. | ✅ No downtime.                | ✅ Automatic rollback.                           | 💲💲 Slightly higher (temporary instances). | Canary testing or production validation.            | Safest for real-world testing with users.       |
| **Blue/Green Deployment**         | Creates a **completely separate environment** (Green) with new version. When verified, **CNAME is swapped** to redirect traffic. | ✅ No downtime.                | ✅ Simple rollback (swap back).                  | 💲💲💲 High (full duplicate environment).   | Mission-critical production releases.               | Most reliable, supports pre-deployment testing. |

---

## 🔹 6. Key Concepts in Elastic Beanstalk

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

### ⚙️ How It Works — Step-by-Step Example

Let’s say you have a **Python web app**.

1. **Create Application** → Name it `MyWebApp`.
2. **Upload Application Version** → Upload a ZIP file of your app (`mywebapp-v1.zip`) → stored in S3.
3. **Create Environment** → Choose “Web Server Environment” tier → Beanstalk launches EC2, Load Balancer, Auto Scaling, and deploys your app.
4. **Monitor & Update** → You can check logs, health metrics, and if you upload a new version (`mywebapp-v2.zip`), Beanstalk can deploy it with zero downtime (rolling updates).
5. **Save Configuration** → If your configuration works well, save it as `MyWebApp-Prod-Config`.
6. **Reuse Platform** → You might choose “Python 3.9 on AL2” as your platform for consistency across all environments.

---

### 🧩 Example Visualization

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
## ⚖️ 7. Traffic Splitting (Canary Deployment)

**Traffic Splitting** is a **deployment strategy** in which **Elastic Beanstalk gradually routes a small percentage of live traffic to the new application version** while most users continue to be served by the old version.

👉 If the new version performs well (no errors, good health), Beanstalk shifts **100% of traffic** to the new version automatically.
👉 If it fails (health check errors or latency increase), Beanstalk **rolls back automatically** to the old version.

It’s like doing a **canary deployment** — testing a new version with real users before fully rolling it out.

---

### ⚙️ How Traffic Splitting Works — Step by Step

1. **Current environment** (e.g., `v1`) is running and healthy.
2. You **deploy a new application version** (e.g., `v2`) using the **Traffic Splitting deployment policy**.
3. Beanstalk temporarily **launches a duplicate set of EC2 instances** with the new version.
4. **A small portion of live traffic** (say 10%) is routed to the new version.
5. Beanstalk **monitors the new version’s health** for a short evaluation period.
6. Based on the results:

   * ✅ If healthy → Beanstalk shifts 100% traffic to the new version.
   * ❌ If unhealthy → Beanstalk routes all traffic back to the old version and terminates the new instances.

---

### 🧩 **Example Scenario**

Imagine you run a **Python Flask web app** called `MyWebApp` using Elastic Beanstalk.

| Step | Description                                                                                           |
| ---- | ----------------------------------------------------------------------------------------------------- |
| 1️⃣  | Your current production environment runs **Version 1.0** (v1) — stable.                               |
| 2️⃣  | You upload **Version 2.0** (v2) with new features.                                                    |
| 3️⃣  | You choose **Deployment Policy → Traffic Splitting**.                                                 |
| 4️⃣  | Beanstalk launches a duplicate environment temporarily and routes **10% of user traffic** to v2.      |
| 5️⃣  | Beanstalk monitors logs, latency, and error rates.                                                    |
| 6️⃣  | If everything is fine for, say, 5 minutes → all traffic moves to v2 and old instances are terminated. |
| 7️⃣  | If there are issues → rollback happens automatically to v1.                                           |

---

### 💡 **Example: Real Use Case**

Let’s say your website serves 10,000 requests/minute.

* You deploy **v2** using Traffic Splitting (10% split).
* For 5 minutes:

  * 9,000 requests → v1 (old version)
  * 1,000 requests → v2 (new version)
* Beanstalk checks for errors (HTTP 5xx, timeouts, latency).
* If healthy → 100% of traffic switches to v2.
* If not → rollback happens seamlessly, without affecting most users.

---

### 🛠️ **Configuration Example**

You can enable traffic splitting via:

#### 1. **Elastic Beanstalk Console:**

* Go to your environment → **Configuration → Rolling updates and deployments**
* Under **Deployment Policy**, select → `Traffic Splitting`

#### 2. **AWS CLI:**

```bash
aws elasticbeanstalk update-environment \
  --environment-name MyWebApp-Prod \
  --version-label v2 \
  --option-settings Namespace=aws:elasticbeanstalk:command,OptionName=DeploymentPolicy,Value=TrafficSplitting
```
---

## 💰 8. Pricing
Elastic Beanstalk itself is **free**, but you pay for the AWS resources it provisions:
- **EC2 instances**
- **Elastic Load Balancer**
- **Auto Scaling**
- **S3 storage**
- **CloudWatch metrics**

> Example: A simple app using 1 `t3.micro` EC2 + ELB may cost only a few dollars/month.

---

## 🧠 9. Practical Example: Deploying a Node.js Web App

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

## ✅ 10. Summary

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
