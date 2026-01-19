
## 1️⃣ IAM – Least Privilege

**Scenario:**
A company wants to ensure that developers can only start and stop EC2 instances but cannot terminate them.

**Which AWS service and feature should be used?**

A. AWS Organizations with SCP <br>
B. IAM user with AdministratorAccess <br>
C. IAM policy attached to a role <br>
D. AWS Shield <br>

✅ **Correct Answer:** **C. IAM policy attached to a role**

📝 **Explanation:**
IAM policies allow you to grant **fine-grained permissions** such as `ec2:StartInstances` and `ec2:StopInstances` while denying `ec2:TerminateInstances`. This follows the **principle of least privilege**.

---

## 2️⃣ Multi-Factor Authentication (MFA)

**Scenario:**
A security audit requires an additional authentication factor for all users accessing the AWS Management Console.

**What should be enabled?**

A. AWS KMS <br>
B. IAM password policy <br>
C. Multi-Factor Authentication (MFA) <br>
D. AWS WAF <br>

✅ **Correct Answer:** **C. Multi-Factor Authentication (MFA)**

📝 **Explanation:**
MFA adds an **extra layer of security** by requiring something the user has (OTP/device) in addition to the password.

---

## 3️⃣ AWS Shield

**Scenario:**
A company’s public website must be protected against **DDoS attacks** at no extra cost.

**Which AWS service should be used?**

A. AWS WAF <br>
B. AWS Shield Standard <br>
C. AWS GuardDuty <br>
D. AWS Firewall Manager <br>

✅ **Correct Answer:** **B. AWS Shield Standard**

📝 **Explanation:**
**AWS Shield Standard** is automatically enabled and provides protection against common DDoS attacks at **no additional cost**.

---

## 4️⃣ AWS WAF – Web Application Protection

**Scenario:**
An application needs protection against **SQL injection and cross-site scripting (XSS)** attacks.

**Which service should be used?**

A. AWS Shield <br>
B. AWS GuardDuty <br>
C. AWS WAF <br>
D. AWS Inspector <br>

✅ **Correct Answer:** **C. AWS WAF**

📝 **Explanation:**
AWS WAF protects web applications by filtering malicious HTTP/HTTPS requests such as SQL injection and XSS.

---

## 5️⃣ AWS KMS – Encryption

**Scenario:**
A company wants to manage encryption keys used to encrypt data stored in S3 and EBS.

**Which service should they use?**

A. AWS Secrets Manager <br>
B. AWS CloudHSM <br>
C. AWS KMS <br>
D. AWS IAM <br>

✅ **Correct Answer:** **C. AWS KMS**

📝 **Explanation:**
**AWS Key Management Service (KMS)** is used to create and manage encryption keys integrated with AWS services.

---

## 6️⃣ AWS Secrets Manager

**Scenario:**
An application needs to securely store and automatically rotate database credentials.

**Which service is BEST suited?**

A. AWS Systems Manager Parameter Store <br>
B. AWS Secrets Manager <br>
C. IAM roles <br>
D. AWS KMS only <br>

✅ **Correct Answer:** **B. AWS Secrets Manager**

📝 **Explanation:**
Secrets Manager securely stores **passwords, API keys**, and supports **automatic rotation**.

---

## 7️⃣ AWS GuardDuty – Threat Detection

**Scenario:**
Security teams want continuous monitoring to detect suspicious API activity and compromised instances.

**Which service should be enabled?**

A. AWS Inspector <br>
B. AWS GuardDuty <br>
C. AWS CloudTrail <br>
D. AWS Config <br>

✅ **Correct Answer:** **B. AWS GuardDuty**

📝 **Explanation:**
GuardDuty uses **machine learning and threat intelligence** to detect malicious or unauthorized behavior.

---

## 8️⃣ AWS CloudTrail – Auditing

**Scenario:**
A company wants to track **who performed which action** on AWS resources.

**Which service provides this information?**

A. AWS Config <br>
B. AWS GuardDuty <br>
C. AWS CloudTrail <br>
D. AWS IAM <br>

✅ **Correct Answer:** **C. AWS CloudTrail**

📝 **Explanation:**
CloudTrail logs **API calls and user activity**, essential for auditing and compliance.

---

## 9️⃣ AWS Config – Compliance

**Scenario:**
An organization wants to continuously monitor whether resources comply with internal security policies.

**Which service should be used?**

A. AWS CloudTrail <br>
B. AWS Config <br>
C. AWS Inspector <br>
D. AWS Trusted Advisor <br>

✅ **Correct Answer:** **B. AWS Config**

📝 **Explanation:**
AWS Config records configuration changes and checks compliance against defined rules.

---

## 🔟 Shared Responsibility Model

**Scenario:**
Who is responsible for **patching the operating system** on an EC2 instance?

A. AWS <br>
B. Customer <br>
C. AWS Support <br>
D. AWS Security Team <br>

✅ **Correct Answer:** **B. Customer**

📝 **Explanation:**
Under the **Shared Responsibility Model**, AWS secures the infrastructure, while **customers secure what they run on AWS**, including EC2 OS patching.

---

### 🎯 Exam Tip for Cloud Practitioner

* **IAM = Identity & Access**
* **WAF = Web attacks**
* **Shield = DDoS**
* **GuardDuty = Threat detection**
* **CloudTrail = Audit logs**
* **Config = Compliance**
* **KMS = Encryption keys**

---
