

## 1️⃣ IAM Least Privilege Access

**Scenario:**
A company wants to allow developers to **only start and stop EC2 instances** in a specific AWS account. They must not be able to terminate instances or access other AWS services.

**Which solution meets this requirement?**

A. Attach the **AmazonEC2FullAccess** managed policy <br>
B. Create an IAM policy allowing `ec2:StartInstances` and `ec2:StopInstances` <br>
C. Assign the developers to the root user <br>
D. Attach a policy with `ec2:*` permissions <br>

**✅ Correct Answer:** **B**

**Explanation:**
Following the **principle of least privilege**, you should grant only the required actions. A custom IAM policy with `ec2:StartInstances` and `ec2:StopInstances` restricts access appropriately.

---

## 2️⃣ Secure Access to AWS Resources from On-Premises

**Scenario:**
An application running on an on-premises server needs **secure temporary access** to upload files to an Amazon S3 bucket without storing long-term AWS credentials.

**What is the BEST solution?**

A. Create an IAM user and store access keys on the server <br>
B. Use AWS STS to assume an IAM role <br>
C. Store credentials in plain text configuration files <br>
D. Use the root user credentials <br>

**✅ Correct Answer:** **B**

**Explanation:**
AWS **Security Token Service (STS)** provides **temporary security credentials**, which is the most secure and recommended approach.

---

## 3️⃣ Encrypting Sensitive Data at Rest

**Scenario:**
A financial application stores sensitive customer data in **Amazon RDS**. The data must be encrypted at rest, and AWS should manage the encryption keys.

**Which solution should you use?**

A. Enable SSL connections only <br>
B. Enable RDS encryption using AWS-managed KMS keys <br>
C. Encrypt data manually at application level <br>
D. Use IAM policies for encryption <br>

**✅ Correct Answer:** **B**

**Explanation:**
Amazon RDS integrates with **AWS Key Management Service (KMS)** to provide **encryption at rest** using AWS-managed keys.

---

## 4️⃣ Protecting Web Applications from Common Attacks

**Scenario:**
A public web application must be protected from **SQL injection and cross-site scripting (XSS)** attacks.

**Which AWS service should be used?**

A. AWS Shield Standard <br>
B. AWS Firewall Manager <br>
C. AWS WAF <br>
D. Amazon GuardDuty <br>

**✅ Correct Answer:** **C**

**Explanation:**
**AWS Web Application Firewall (WAF)** protects applications from common web exploits such as SQL injection and XSS.

---

## 5️⃣ DDoS Protection for a Production Application

**Scenario:**
A company runs a critical production workload using Amazon CloudFront and Application Load Balancer. They want **advanced DDoS protection** and 24/7 support.

**Which solution should they choose?**

A. AWS WAF <br>
B. AWS Shield Standard <br>
C. AWS Shield Advanced <br>
D. Amazon Inspector <br>

**✅ Correct Answer:** **C**

**Explanation:**
**AWS Shield Advanced** provides enhanced DDoS protection, cost protection, and access to AWS DDoS Response Team (DRT).

---

## 6️⃣ Continuous Threat Detection

**Scenario:**
A security team wants to continuously monitor AWS accounts for **malicious activity**, compromised instances, and unusual API calls.

**Which AWS service meets this requirement?**

A. AWS CloudTrail <br>
B. Amazon Inspector <br>
C. Amazon GuardDuty <br>
D. AWS Config <br>

**✅ Correct Answer:** **C**

**Explanation:**
**Amazon GuardDuty** uses machine learning and threat intelligence to detect suspicious activity.

---

## 7️⃣ Tracking Configuration Changes for Compliance

**Scenario:**
An organization must **track and record configuration changes** to AWS resources to meet compliance requirements.

**Which AWS service should be used?**

A. AWS CloudTrail <br>
B. AWS Config <br>
C. Amazon GuardDuty <br>
D. AWS WAF <br>

**✅ Correct Answer:** **B**

**Explanation:**
**AWS Config** records configuration changes and evaluates them against compliance rules.

---

## 8️⃣ Auditing API Activity

**Scenario:**
A security auditor needs a history of **all API calls** made in an AWS account, including the user and source IP.

**Which service provides this information?**

A. AWS Config <br>
B. Amazon CloudWatch <br>
C. AWS CloudTrail <br>
D. AWS IAM Access Analyzer <br>

**✅ Correct Answer:** **C**

**Explanation:**
**AWS CloudTrail** logs all API activity across AWS services for auditing and security analysis.

---

## 9️⃣ Secure Secrets Management

**Scenario:**
An application needs to store **database credentials securely** and rotate them automatically.

**Which AWS service is BEST suited?**

A. AWS KMS <br>
B. AWS Secrets Manager <br>
C. Amazon S3 <br> 
D. AWS Systems Manager Parameter Store (Standard) <br>

**✅ Correct Answer:** **B**

**Explanation:**
**AWS Secrets Manager** securely stores secrets and supports **automatic rotation**, ideal for database credentials.

---

## 🔟 Cross-Account Resource Access

**Scenario:**
A company wants to allow users in **Account A** to access an S3 bucket in **Account B** securely.

**What is the BEST approach?**

A. Share root credentials <br>
B. Create an IAM role in Account B and allow Account A to assume it <br>
C. Create IAM users in both accounts <br>
D. Use AWS Shield <br>

**✅ Correct Answer:** **B**

**Explanation:**
**IAM roles with cross-account trust policies** are the most secure and recommended solution.

---

### 🔑 Exam Tips for Security, Identity & Compliance

* Always think **Least Privilege**
* Prefer **IAM Roles over IAM Users**
* Know the difference between **CloudTrail vs Config vs GuardDuty**
* **WAF = Web attacks**, **Shield = DDoS**
* **KMS = Encryption**, **Secrets Manager = Credentials**
---
