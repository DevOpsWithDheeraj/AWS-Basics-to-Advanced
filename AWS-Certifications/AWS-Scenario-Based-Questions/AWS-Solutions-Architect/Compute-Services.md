# AWS Certified Solutions Architect – Associate

## Scenario-Based Questions on **AWS Compute Services**

---

### **Question 1: Choosing the Right EC2 Purchasing Option**

A fintech company runs a risk-analysis application that executes **every night for 6 hours**. The workload is predictable and will run for at least **one year**. Cost optimization is a priority, but the application **cannot be interrupted**.

**Which EC2 pricing option should you choose?**

A. On-Demand Instances
B. Spot Instances
C. Reserved Instances (Standard, 1-year)
D. Dedicated Hosts

✅ **Correct Answer: C**

**Explanation:**
Standard Reserved Instances provide significant cost savings (up to ~72%) for steady, predictable workloads. Spot Instances can be interrupted, making them unsuitable. Dedicated Hosts are expensive and used for compliance or licensing needs.

---

### **Question 2: High Availability for Web Application**

A company hosts a public web application on EC2. The application must remain available even if an Availability Zone fails.

**Which architecture meets this requirement?**

A. Single EC2 instance with Elastic IP
B. EC2 instances in multiple AZs behind an Application Load Balancer
C. EC2 instance with scheduled snapshots
D. EC2 Auto Scaling in a single AZ

✅ **Correct Answer: B**

**Explanation:**
Deploying EC2 instances across multiple AZs behind an Application Load Balancer ensures fault tolerance and high availability. A single AZ setup is a single point of failure.

---

### **Question 3: Automatically Scaling Compute Capacity**

An e-commerce application experiences **traffic spikes during sales events**. The company wants EC2 instances to scale automatically based on demand.

**Which solution is MOST appropriate?**

A. AWS Elastic Beanstalk
B. EC2 Auto Scaling with Application Load Balancer
C. AWS Lambda
D. Manual instance launch using AMIs

✅ **Correct Answer: B**

**Explanation:**
EC2 Auto Scaling automatically adjusts the number of EC2 instances based on metrics like CPU utilization. ALB distributes traffic evenly. Lambda is event-driven and not suitable for full web servers in this case.

---

### **Question 4: Cost-Optimized Fault-Tolerant Batch Processing**

A data analytics team runs batch jobs that can tolerate interruptions. Jobs can restart from checkpoints.

**Which EC2 option is MOST cost-effective?**

A. On-Demand Instances
B. Reserved Instances
C. Spot Instances
D. Dedicated Instances

✅ **Correct Answer: C**

**Explanation:**
Spot Instances provide the lowest cost and are ideal for fault-tolerant workloads. Since the jobs can restart, interruptions are acceptable.

---

### **Question 5: Running Containers on AWS**

A company wants to run **Docker containers** without managing EC2 instances or servers.

**Which compute service should be used?**

A. Amazon EC2 with Docker installed
B. Amazon ECS with EC2 launch type
C. AWS Lambda
D. Amazon ECS with AWS Fargate

✅ **Correct Answer: D**

**Explanation:**
AWS Fargate is a **serverless compute engine for containers**. It removes the need to manage EC2 instances while running containers.

---

### **Question 6: Short-Lived Event-Driven Compute**

An application processes image uploads. Code should run **only when an image is uploaded** and scale automatically.

**Which compute service is BEST suited?**

A. EC2 Auto Scaling
B. AWS Lambda
C. Elastic Beanstalk
D. Amazon ECS

✅ **Correct Answer: B**

**Explanation:**
AWS Lambda is event-driven, automatically scales, and charges only for execution time. It is ideal for short-lived tasks like image processing.

---

### **Question 7: Compliance Requirement for Physical Server Control**

A company requires **physical isolation and control over the underlying hardware** due to licensing restrictions.

**Which EC2 option should be used?**

A. Reserved Instances
B. Spot Instances
C. Dedicated Hosts
D. On-Demand Instances

✅ **Correct Answer: C**

**Explanation:**
Dedicated Hosts provide visibility and control over the physical server, which is required for certain compliance and licensing needs.

---

### **Question 8: Reducing Operational Overhead**

A startup wants to deploy a web application quickly without managing infrastructure, load balancers, or scaling policies.

**Which service should they use?**

A. EC2 with Auto Scaling
B. AWS Elastic Beanstalk
C. Amazon ECS
D. AWS Lambda

✅ **Correct Answer: B**

**Explanation:**
Elastic Beanstalk is a Platform as a Service (PaaS) that automatically handles deployment, scaling, monitoring, and infrastructure management.

---

### **Question 9: Improving EC2 Instance Security**

An architect wants to provide EC2 instances **temporary credentials** to access AWS services without storing access keys.

**What is the BEST solution?**

A. Store access keys in environment variables
B. Use IAM user credentials
C. Attach an IAM role to the EC2 instance
D. Use AWS KMS

✅ **Correct Answer: C**

**Explanation:**
IAM roles provide temporary credentials securely via the instance metadata service. This is an AWS best practice.

---

### **Question 10: Compute for Machine Learning Training**

A machine learning team requires **GPU-based compute** for training deep learning models.

**Which EC2 instance family is MOST appropriate?**

A. T family
B. M family
C. C family
D. P family

✅ **Correct Answer: D**

**Explanation:**
P family instances are optimized for GPU-based workloads like machine learning and high-performance computing.

---

### ✅ **Exam Tip**

For the **Solutions Architect – Associate** exam, focus on:

* High availability (Multi-AZ designs)
* Cost optimization (Spot vs Reserved vs On-Demand)
* Choosing the right compute service (EC2, Lambda, ECS, Fargate, Elastic Beanstalk)
* Security best practices (IAM roles)

---
