# AWS-Basics-to-Advanced

## ☁️ **1. AWS Core Concepts**

* What is Cloud Computing
* AWS Global Infrastructure (Regions, AZs, Edge Locations)
* Shared Responsibility Model
* AWS Management Console & CLI

---

## 🖥️ **2. Compute Services**

* **EC2 (Elastic Compute Cloud)**

  * What is EC2, Instance Types
  * EBS Volume vs Instance Store
  * AMI, Security Group, Key Pair, Tags
  * Pricing Models (On-demand, Reserved, Spot, Savings Plans)
  * **Difference between Security Group & NACLs**

* **AWS Batch** – Running large-scale batch computing jobs with EC2 or Fargate

* **Elastic Beanstalk** – Automated app deployment (e.g., Python, Java, Node.js apps)

* **Lambda** – Serverless compute with pay-per-invocation

  * Examples of Lambda use cases
  * Optimization strategies

* **Fargate** – Serverless container compute for ECS/EKS

  * Examples and comparison with EC2 and Lambda

* **AWS SAR (Serverless Application Repository)** – Deploy reusable Lambda-based apps

---

## 🗃️ **3. Storage Services**

* **S3 (Simple Storage Service)** – Object storage with versioning & lifecycle rules
* **EBS (Elastic Block Store)** – Persistent block storage for EC2
* **EFS (Elastic File System)** – Shared file storage for Linux EC2 instances
* **FSx (Windows/Linux File Systems)**
* **Glacier** – Low-cost cold storage for archival
* **Storage Gateway** – Hybrid cloud storage bridge
* **AWS Backup** – Centralized backup management
* **Snow Family** – Physical data transport solutions

---

## 🗄️ **4. Database Services**

* **RDS (Relational Database Service)** – Managed relational databases (MySQL, PostgreSQL, Oracle, SQL Server, MariaDB, Aurora)
* **DynamoDB** – Fully managed NoSQL key-value database
* **Redshift** – Data warehouse for analytics and BI workloads
* **ElastiCache** – In-memory caching service (Redis and Memcached)
* **Neptune** – Managed graph database for connected data
* **DocumentDB** – Managed document-oriented database compatible with MongoDB
* **Aurora** – High-performance relational database compatible with MySQL and PostgreSQL

---

## 🧩 **5. Networking & Content Delivery**

* **VPC (Virtual Private Cloud)**

  * Subnets, Route Tables, Internet Gateway, NAT Gateway
  * Security Groups vs NACLs
* **Elastic Load Balancer (ELB)** – Types: Classic, ALB, NLB
* **Route 53** – DNS and Domain management
* **AWS Direct Connect** – Dedicated network connection to AWS

---

## 🔐 **6. Security, Identity & Compliance**

* **IAM (Identity and Access Management)**

  * Users, Groups, Roles, Policies
  * IAM Best Practices
* **KMS (Key Management Service)** – Encryption key creation & management

---

## 🧱 **7. Infrastructure as Code (IaC)**

* **AWS CloudFormation** – Automating infrastructure deployment using templates

---

## ⚙️ **8. Application Integration**

* **SQS (Simple Queue Service)**
* **SNS (Simple Notification Service)**
* **EventBridge (CloudWatch Events)**

---

## 🚀 **9. Deployment & CI/CD**

* **AWS CodeCommit** – Source control repository
* **AWS CodeBuild** – Build automation
* **AWS CodeDeploy** – Deployment automation
* **AWS CodePipeline** – CI/CD orchestration

---

## 📊 **10. Monitoring & Management**

* **CloudWatch** – Logs, Metrics, Alarms
* **CloudTrail** – API activity tracking
* **Trusted Advisor** – Cost, Security, and Performance recommendations
* **AWS Config** – Configuration compliance tracking

---

## 🧩 **11. Containers & Kubernetes**

* **ECS (Elastic Container Service)**
* **EKS (Elastic Kubernetes Service)**
* Integration with Fargate and EC2

---

## 💰 **12. Billing & Cost Management Services**

* **AWS Billing Console** – Centralized view of account charges and usage
* **Cost Explorer** – Analyze spending trends and forecast future costs
* **AWS Budgets** – Set custom budgets and receive alerts on spending limits
* **AWS Pricing Calculator** – Estimate costs before deploying resources
* **Consolidated Billing** – Combine multiple AWS accounts for unified billing
* **Savings Plans & Reserved Instances** – Cost optimization options for long-term workloads

---
