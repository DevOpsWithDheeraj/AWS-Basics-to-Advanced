# AWS Monitoring and Auditing Services

**AWS Monitoring and Auditing Services** provide tools to continuously observe, analyze, and record activities across your AWS environment.
They help ensure **performance efficiency**, **operational visibility**, **security compliance**, and **accountability** by monitoring resources, tracking configuration changes, and auditing user actions in real time.

---

## 🔍 **1. Amazon CloudWatch — Monitoring**

### 📘 **Purpose:**

CloudWatch is AWS’s primary **monitoring and observability service**. It collects **metrics, logs, and events** from AWS resources and applications to help you understand performance and detect operational issues.

### ⚙️ **Key Features:**

* Monitor CPU, memory, disk usage, latency, etc.
* Create **alarms** to trigger notifications or automated actions.
* Visualize data using **dashboards**.
* Automatically react using **CloudWatch Events/Rules**.

### 💡 **Example:**

* You have an EC2 instance running a web app.
  → CloudWatch tracks **CPU Utilization** and **Network In/Out**.
  → You set an alarm: if CPU > 80% for 5 mins → **Auto Scaling** adds another instance or sends an **SNS alert** to admins.

---

## 🧾 **2. AWS CloudTrail — Auditing**

### 📘 **Purpose:**

CloudTrail records **all API calls** made within your AWS account — who did what, when, from where, and which resource was affected.
It provides **governance, compliance, and security auditing**.

### ⚙️ **Key Features:**

* Tracks console, CLI, SDK, and API calls.
* Delivers logs to an S3 bucket.
* Integrates with CloudWatch for real-time alerts.

### 💡 **Example:**

* An IAM user accidentally deleted an S3 bucket.
  → CloudTrail shows: `DeleteBucket` action performed by **user: devops_admin**, from **IP: 203.x.x.x**, at **11:32 AM**.
  → Helps in root-cause analysis and security auditing.

---

## 🧩 **3. AWS Config — Resource Configuration Tracking**

### 📘 **Purpose:**

AWS Config tracks **configuration changes** of AWS resources and checks whether they **comply with organizational policies**.

### ⚙️ **Key Features:**

* Tracks configuration history of each resource (EC2, S3, IAM, etc.).
* Defines **Config Rules** for compliance checks.
* Can trigger remediation actions.

### 💡 **Example:**

* You set a Config Rule: “S3 buckets must not be public.”
  → If someone makes a bucket public, AWS Config marks it as **non-compliant** and can automatically **remove public access** or **notify via SNS**.

---

## 🧠 **4. AWS Trusted Advisor — Optimization & Best Practices**

### 📘 **Purpose:**

Trusted Advisor analyzes your AWS environment and gives recommendations for **cost optimization, performance, security, fault tolerance, and service limits**.

### ⚙️ **Key Features:**

* Offers checks in 5 categories:

  * Cost Optimization
  * Performance
  * Security
  * Fault Tolerance
  * Service Limits

### 💡 **Example:**

* Trusted Advisor finds unused EBS volumes or idle EC2 instances.
  → Suggests deleting them to save cost.
  → It may also warn that an S3 bucket is **publicly accessible**, violating security best practices.

---

## 🛡️ **5. Amazon Inspector — Security Vulnerability Assessment**

### 📘 **Purpose:**

Inspector automatically scans AWS resources for **security vulnerabilities** and **deviation from best practices**.

### ⚙️ **Key Features:**

* Scans EC2 instances for outdated packages or open ports.
* Checks container images in ECR for vulnerabilities.
* Integrates with Security Hub for centralized findings.

### 💡 **Example:**

* You run a web app on EC2.
  → Inspector scans it and reports that Apache version is outdated and vulnerable (CVE found).
  → You patch the instance to fix the issue.

---

## 🌐 **6. VPC Flow Logs — Network Monitoring**

### 📘 **Purpose:**

VPC Flow Logs capture **IP traffic information** going in and out of your AWS resources (VPC, Subnets, or ENIs).

### ⚙️ **Key Features:**

* Helps troubleshoot connectivity and security issues.
* Stores data in **CloudWatch Logs** or **S3**.
* Can identify blocked connections or suspicious activity.

### 💡 **Example:**

* Your EC2 can’t reach a database.
  → You enable Flow Logs for the subnet.
  → Logs show that traffic to the DB port (3306) is being **denied by a security group**.
  → You fix the rule accordingly.

---

## 📊 **Summary Table**

| **Service**         | **Category**       | **Purpose**                                | **Example Use Case**                 |
| ------------------- | ------------------ | ------------------------------------------ | ------------------------------------ |
| **CloudWatch**      | Monitoring         | Collects & visualizes metrics/logs         | Monitor EC2 CPU, trigger alarms      |
| **CloudTrail**      | Auditing           | Tracks API calls (who did what)            | Investigate resource deletion        |
| **AWS Config**      | Compliance         | Tracks resource configuration & compliance | Ensure S3 buckets aren’t public      |
| **Trusted Advisor** | Optimization       | Recommends best practices                  | Identify idle EC2s & security issues |
| **Inspector**       | Security Scanning  | Detects vulnerabilities                    | Scan EC2 & ECR for CVEs              |
| **VPC Flow Logs**   | Network Monitoring | Captures network traffic info              | Diagnose denied connections          |

---
