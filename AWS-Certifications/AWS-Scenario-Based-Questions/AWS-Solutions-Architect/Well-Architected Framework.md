
## 🔹 1. Operational Excellence

### **Question 1**

A company runs a web application on EC2 instances behind an Application Load Balancer. The operations team wants to **quickly identify and fix issues** when deployments cause failures. Which solution BEST follows the **Operational Excellence** pillar?

**A.** Enable AWS Trusted Advisor <br>
**B.** Use AWS CloudTrail to log API calls <br>
**C.** Implement AWS CloudWatch alarms and AWS Systems Manager runbooks <br>
**D.** Enable AWS Shield Standard <br>

✅ **Correct Answer:** **C**

### **Explanation**

* CloudWatch alarms detect failures automatically.
* Systems Manager runbooks allow automated remediation.
* This aligns with **monitoring, automation, and incident response**, key principles of Operational Excellence.

---

## 🔹 2. Security

### **Question 2**

An application stores sensitive customer data in Amazon S3. The security team wants to **ensure encryption, least-privilege access, and auditability**. Which solution BEST satisfies the **Security** pillar?

**A.** Enable S3 versioning and MFA Delete <br>
**B.** Encrypt data using AWS KMS, use IAM roles, and enable CloudTrail <br>
**C.** Use Amazon CloudFront with HTTPS <br>
**D.** Enable AWS Shield Advanced <br>

✅ **Correct Answer:** **B**

### **Explanation**

* AWS KMS ensures encryption at rest.
* IAM roles enforce least-privilege access.
* CloudTrail provides auditing and logging.
* This directly matches **Security pillar best practices**.

---

## 🔹 3. Reliability

### **Question 3**

A company wants its application to **automatically recover from instance failures** and remain available during outages. Which design BEST follows the **Reliability** pillar?

**A.** Run the application on a single large EC2 instance <br>
**B.** Use EC2 instances in multiple Availability Zones with Auto Scaling <br>
**C.** Use Amazon S3 to store application logs <br>
**D.** Use AWS Snowball for backups <br>

✅ **Correct Answer:** **B**

### **Explanation**

* Multi-AZ deployment improves fault tolerance.
* Auto Scaling replaces unhealthy instances automatically.
* This supports **failure recovery and high availability**, key Reliability principles.

---

## 🔹 4. Performance Efficiency

### **Question 4**

An application experiences unpredictable traffic spikes. The architect wants to **optimize performance while minimizing manual intervention**. Which solution BEST aligns with the **Performance Efficiency** pillar?

**A.** Use larger EC2 instances permanently <br>
**B.** Enable EC2 Auto Scaling and use Elastic Load Balancing <br>
**C.** Move the application to a single Availability Zone <br>
**D.** Use AWS Snowcone for compute workloads <br>

✅ **Correct Answer:** **B**

### **Explanation**

* Auto Scaling dynamically adjusts capacity.
* Load Balancer distributes traffic efficiently.
* This ensures **right-sizing and scalability**, core Performance Efficiency concepts.

---

## 🔹 5. Cost Optimization

### **Question 5**

A batch processing job runs every night for 6 hours. The workload is flexible and can tolerate interruptions. Which option MOST cost-effectively follows the **Cost Optimization** pillar?

**A.** Use On-Demand EC2 instances <br>
**B.** Use Reserved Instances <br>
**C.** Use EC2 Spot Instances <br>
**D.** Use Dedicated Hosts <br>

✅ **Correct Answer:** **C**

### **Explanation**

* Spot Instances offer up to **90% cost savings**.
* Suitable for **interruptible workloads**.
* This demonstrates **cost-aware resource selection**.

---

## 🔹 6. Sustainability

### **Question 6**

A company wants to reduce its **environmental impact** while maintaining performance. Which design BEST aligns with the **Sustainability** pillar?

**A.** Run workloads continuously on oversized instances <br>
**B.** Use serverless services like AWS Lambda and DynamoDB <br>
**C.** Deploy resources in multiple Regions unnecessarily <br>
**D.** Use Dedicated EC2 hosts <br>

✅ **Correct Answer:** **B**

### **Explanation**

* Serverless services scale automatically and use resources efficiently.
* Reduced idle capacity lowers energy consumption.
* Sustainability focuses on **efficient resource usage**.

---

## 🔹 7. Mixed Pillars (Common in Exam)

### **Question 7**

A production application must be **secure, highly available, and cost-efficient**. Which architecture BEST follows the **AWS Well-Architected Framework**?

**A.** Single EC2 instance with manual backups <br>
**B.** Multi-AZ architecture, IAM roles, Auto Scaling, and CloudWatch monitoring <br>
**C.** Dedicated hosts with static capacity <br>
**D.** On-premises backup with manual scaling <br>

✅ **Correct Answer:** **B**

### **Explanation**

This option addresses:

* **Security:** IAM roles
* **Reliability:** Multi-AZ
* **Performance:** Auto Scaling
* **Operational Excellence:** Monitoring
* **Cost Optimization:** Avoids over-provisioning

---

## 📌 Exam Tip for SAA

For **Well-Architected questions**, always think:

* **Automate**
* **Scale automatically**
* **Design for failure**
* **Least privilege**
* **Pay only for what you use**
* **Avoid single points of failure**

---
