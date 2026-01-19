Here are **scenario-based questions from AWS Compute Services** for the **AWS Certified Cloud Practitioner (CLF-C02)** exam.
Each question includes **options, correct answer, and a clear explanation** 👇

---

## 1️⃣ Choosing a virtual server in the cloud

A startup wants to quickly launch a web application on a virtual server where they can control the operating system and install custom software.

**Which AWS service should they use?**

A. AWS Lambda
B. Amazon EC2
C. Amazon RDS
D. AWS Elastic Beanstalk

✅ **Correct Answer:** **B. Amazon EC2**

**Explanation:**
Amazon EC2 provides resizable virtual servers where customers control the OS, storage, and installed applications. Lambda does not allow OS control, and RDS is for databases.

---

## 2️⃣ Running code without managing servers

A developer wants to run backend code in response to HTTP requests without provisioning or managing servers. The application should automatically scale.

**Which compute service is MOST suitable?**

A. Amazon EC2
B. Amazon ECS
C. AWS Lambda
D. AWS Batch

✅ **Correct Answer:** **C. AWS Lambda**

**Explanation:**
AWS Lambda is a **serverless compute service** that runs code in response to events and automatically scales. No infrastructure management is required.

---

## 3️⃣ Containerized application management

A company is running Docker containers and wants AWS to manage the container orchestration without managing EC2 instances.

**Which service should they use?**

A. Amazon EC2
B. Amazon ECS with EC2 launch type
C. Amazon EKS
D. Amazon ECS with AWS Fargate

✅ **Correct Answer:** **D. Amazon ECS with AWS Fargate**

**Explanation:**
AWS Fargate is a **serverless compute engine for containers**, removing the need to manage EC2 instances.

---

## 4️⃣ Batch processing workload

A research team needs to process large volumes of data jobs that can run at any time and do not require immediate results.

**Which AWS compute service is BEST suited?**

A. AWS Lambda
B. Amazon EC2 Auto Scaling
C. AWS Batch
D. Amazon Lightsail

✅ **Correct Answer:** **C. AWS Batch**

**Explanation:**
AWS Batch efficiently runs **batch computing workloads**, automatically provisioning optimal compute resources.

---

## 5️⃣ Simplified virtual server for beginners

A small business wants a simple, low-cost virtual server with bundled storage and networking for hosting a basic website.

**Which AWS service should they choose?**

A. Amazon EC2
B. Amazon Lightsail
C. AWS Lambda
D. Amazon ECS

✅ **Correct Answer:** **B. Amazon Lightsail**

**Explanation:**
Amazon Lightsail offers **simplified virtual servers** with predictable pricing, ideal for small websites and beginners.

---

## 6️⃣ High availability for EC2 instances

An application must remain available even if one EC2 instance fails.

**Which AWS feature helps achieve this?**

A. Elastic Load Balancer
B. Amazon S3
C. AWS Snowball
D. Amazon CloudFront

✅ **Correct Answer:** **A. Elastic Load Balancer**

**Explanation:**
Elastic Load Balancing distributes traffic across multiple EC2 instances, improving **availability and fault tolerance**.

---

## 7️⃣ Automatic scaling based on demand

A company expects unpredictable traffic spikes and wants EC2 instances to scale automatically.

**Which AWS service should they use?**

A. AWS Lambda
B. Amazon EC2 Auto Scaling
C. Amazon CloudWatch Logs
D. AWS Batch

✅ **Correct Answer:** **B. Amazon EC2 Auto Scaling**

**Explanation:**
EC2 Auto Scaling automatically **adds or removes EC2 instances** based on defined conditions such as CPU usage.

---

## 8️⃣ Short-running event-driven task

An image upload should trigger thumbnail generation automatically.

**Which compute service is MOST appropriate?**

A. Amazon EC2
B. AWS Lambda
C. Amazon ECS
D. Amazon Lightsail

✅ **Correct Answer:** **B. AWS Lambda**

**Explanation:**
AWS Lambda is ideal for **event-driven, short-duration tasks**, such as processing uploaded images.

---

## 9️⃣ Kubernetes-based workloads

A company wants to run Kubernetes clusters managed by AWS.

**Which service should they use?**

A. Amazon ECS
B. Amazon EKS
C. AWS Lambda
D. Amazon Lightsail

✅ **Correct Answer:** **B. Amazon EKS**

**Explanation:**
Amazon EKS is AWS’s **managed Kubernetes service**, reducing the operational effort of running Kubernetes.

---

## 🔟 Paying only for execution time

Which compute service charges you **only for the time your code runs**?

A. Amazon EC2
B. Amazon Lightsail
C. AWS Lambda
D. Amazon ECS

✅ **Correct Answer:** **C. AWS Lambda**

**Explanation:**
AWS Lambda follows a **pay-per-use model**, charging only for execution duration and number of requests.

---

### 📌 Exam Tip for Cloud Practitioner

Remember these quick associations:

* **EC2** → Virtual servers
* **Lambda** → Serverless, event-driven
* **ECS / EKS** → Containers
* **Fargate** → Serverless containers
* **Lightsail** → Simple VPS
* **Batch** → Large-scale batch jobs
