
## **Question 1: ECS vs EKS (Managed Simplicity)**

A startup wants to run containerized applications on AWS with **minimal operational overhead**. The team does not want to manage Kubernetes control planes or worker node upgrades.

Which solution should a solutions architect recommend?

A. Amazon EKS with self-managed nodes <br>
B. Amazon ECS with AWS Fargate <br>
C. Amazon EKS with Fargate <br>
D. Amazon EC2 with Docker installed <br>

✅ **Correct Answer:** **B. Amazon ECS with AWS Fargate**

### **Explanation:**

* **ECS + Fargate** is the **simplest container option** on AWS.
* No cluster management, no EC2 instances, no Kubernetes complexity.
* AWS manages compute, scaling, and infrastructure.
* Best for teams wanting **low operational effort**.

---

## **Question 2: Cost Optimization for Long-Running Containers**

A company runs a **long-running container workload** that requires predictable compute capacity. Cost optimization is a high priority.

Which option is MOST cost-effective?

A. ECS on Fargate <br>
B. EKS on Fargate <br>
C. ECS on EC2 with Reserved Instances <br>
D. EKS with AWS Lambda <br>

✅ **Correct Answer:** **C. ECS on EC2 with Reserved Instances**

### **Explanation:**

* EC2 **Reserved Instances** provide significant savings for steady workloads.
* Fargate is convenient but more expensive for long-running tasks.
* Lambda is not suitable for long-running container workloads.

---

## **Question 3: High Availability Container Deployment**

A containerized web application must be **highly available** and **automatically scale across multiple Availability Zones**.

Which architecture meets these requirements?

A. Single ECS task running on one EC2 instance <br>
B. ECS service using Application Load Balancer across multiple AZs <br>
C. Docker containers on a single EC2 instance <br>
D. EKS cluster in a single Availability Zone <br>

✅ **Correct Answer:** **B. ECS service using Application Load Balancer across multiple AZs**

### **Explanation:**

* ECS services automatically maintain desired task count.
* ALB distributes traffic across AZs.
* Ensures **fault tolerance and auto-scaling**.

---

## **Question 4: Kubernetes Requirement**

A company must deploy container workloads using **Kubernetes** because of existing tooling and expertise.

Which AWS service should be used?

A. Amazon ECS <br>
B. AWS Fargate <br>
C. Amazon EKS <br>
D. Amazon EC2 Auto Scaling <br>

✅ **Correct Answer:** **C. Amazon EKS**

### **Explanation:**

* **Amazon EKS** is AWS’s managed Kubernetes service.
* ECS does not use Kubernetes.
* Fargate is a compute option, not a container orchestration platform.

---

## **Question 5: Serverless Containers**

A development team wants to run containers **without managing servers or clusters** and wants to pay **only for running containers**.

Which solution should be selected?

A. ECS on EC2 <br>
B. EKS on EC2 <br>
C. ECS on AWS Fargate <br>
D. EC2 Auto Scaling with Docker <br>

✅ **Correct Answer:** **C. ECS on AWS Fargate**

### **Explanation:**

* Fargate is **serverless compute for containers**.
* No EC2 instances to manage.
* You pay per vCPU and memory used.

---

## **Question 6: Image Storage and Versioning**

A company wants a **secure, highly available** repository to store and version Docker images with **fine-grained access control**.

Which AWS service should be used?

A. Amazon S3 <br>
B. AWS CodeCommit <br>
C. Amazon ECR <br>
D. Amazon ECS <br>

✅ **Correct Answer:** **C. Amazon ECR**

### **Explanation:**

* **Amazon Elastic Container Registry (ECR)** is designed for container images.
* Supports IAM-based access control.
* Integrates seamlessly with ECS and EKS.

---

## **Question 7: Blue/Green Deployment for Containers**

A company wants to perform **blue/green deployments** for an ECS service with minimal downtime.

Which AWS service enables this?

A. Amazon Route 53 <br>
B. AWS CodeDeploy <br>
C. AWS Auto Scaling <br>
D. AWS CloudFormation <br>

✅ **Correct Answer:** **B. AWS CodeDeploy**

### **Explanation:**

* CodeDeploy supports **blue/green deployments** for ECS.
* Enables traffic shifting and rollback.
* Reduces deployment risk.

---

## **Question 8: Secure Communication Between Containers**

Multiple ECS tasks need to **securely communicate** with each other within a VPC.

What is the BEST approach?

A. Use public IPs for each container <br>
B. Use security groups and private subnets <br>
C. Expose containers via internet-facing ALB <br>
D. Use AWS Global Accelerator <br>

✅ **Correct Answer:** **B. Use security groups and private subnets**

### **Explanation:**

* Containers in private subnets are not internet accessible.
* Security groups control inbound and outbound traffic.
* Best practice for **secure internal communication**.

---

## **Question 9: Auto Scaling Containers Based on Load**

A containerized application experiences traffic spikes. The team wants **automatic scaling** based on CPU usage.

Which feature should be used?

A. EC2 Auto Scaling only <br>
B. ECS Service Auto Scaling <br>
C. AWS Lambda concurrency <br>
D. CloudFormation stack updates <br>

✅ **Correct Answer:** **B. ECS Service Auto Scaling**

### **Explanation:**

* ECS Service Auto Scaling scales tasks based on CloudWatch metrics.
* Supports CPU, memory, and custom metrics.
* Ideal for dynamic workloads.

---

## **Question 10: When to Choose EKS over ECS**

Which scenario BEST justifies choosing **Amazon EKS** instead of ECS?

A. Simple microservice with no orchestration needs <br>
B. Team wants deep Kubernetes ecosystem integration <br>
C. Lowest cost container service <br>
D. Small development team with no container experience <br>

✅ **Correct Answer:** **B. Team wants deep Kubernetes ecosystem integration**

### **Explanation:**

* EKS is ideal when Kubernetes features, tools, and portability are required.
* ECS is simpler but AWS-specific.
* EKS supports multi-cloud portability and Kubernetes-native tooling.

---

### 🔑 **Exam Tip for Containers (SAA-C03)**

* **ECS + Fargate** → Simplicity, serverless
* **ECS + EC2** → Cost optimization
* **EKS** → Kubernetes requirement
* **ECR** → Container image storage
* **ALB + ECS** → High availability & scaling

---
