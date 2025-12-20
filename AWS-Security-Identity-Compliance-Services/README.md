#  AWS Security, Identity & Compliance Services

Security in AWS follows **shared responsibility**:

* **AWS secures the cloud** (hardware, network, hypervisor).
* **You secure workloads in the cloud** (IAM, encryption, firewalls, patching).

Below are the core AWS services that help you secure apps, data, networks, and identities.

---

## 🔐 **1. AWS IAM – Identity and Access Management**

### **Purpose:**

Control *who* can do *what* in your AWS account.

### **What it provides:**

* IAM Users, Groups, Roles
* Fine-grained policies (JSON)
* MFA, Access Analyzer
* Temporary credentials using Roles

### **Example:**

Your DevOps team deploys to EC2 using GitHub Actions.
You don't want to store AWS keys in the repository.
So, you create:

* **IAM Role** → “GitHubDeployRole”
* Give only `ec2:StartInstances`, `ec2:StopInstances`
* GitHub OIDC authenticates → gets **temporary creds**

**Result:** Secure, keyless deployments.

---

## 🔑 **2. AWS KMS – Key Management Service**

### **Purpose:**

Create and manage encryption keys.

### **Used for:**

* Encrypting S3 data
* EBS volume encryption
* RDS, DynamoDB encryption
* Secrets Manager
* TLS certificates through ACM (indirectly)

### **Example:**

You store customer reports in S3.
To protect data:

* Enable **S3 Server-Side Encryption** (SSE-KMS)
* Create a **customer-managed CMK**
* Allow only finance-role to decrypt

**Result:**
Even if S3 objects leak → without KMS key access, data is unreadable.

---

## 🛡️ **3. AWS WAF – Web Application Firewall**

### **Purpose:**

Protect web applications at **HTTP/HTTPS layer (Layer 7).**

### **Blocks:**

* SQL Injection
* Cross-site scripting
* Bot attacks
* Bad IPs
* Rate limiting

### **Where it attaches:**

* CloudFront
* Application Load Balancer
* API Gateway
* AppSync

### **Example:**

Your EKS application faces bot traffic.
You attach:

* AWS WAF → Enable **“Bot Control” rule**
* Add **Rate-Limiting rule: 100 req/min per IP**

**Result:** Scrapers and bots get blocked.

---

## 🛡️ **4. AWS Shield – DDoS Protection**

### **Levels:**

1. **Shield Standard** (Free)

   * Automatic DDoS protection for CloudFront, Route 53, ALB
2. **Shield Advanced** (Paid)

   * 24/7 DDoS Response Team
   * Cost protection
   * WAF integration
   * Real-time attack visibility

### **Example:**

Your e-commerce site behind CloudFront gets a 10M req/sec DDoS attack.

* **Shield Standard** absorbs most of it.
* With **Shield Advanced**, AWS also blocks pattern-based attacks and refunds scaling costs.

---

## 🕵️ **5. AWS Macie – Sensitive Data Discovery**

### **Purpose:**

Automatically finds sensitive data such as:

* PII (emails, names, Aadhaar-like IDs)
* Credit card numbers
* Secrets in files

### **Example:**

Your S3 bucket contains logs uploaded by users.
You run Macie → It finds:

* Passwords stored inside logs
* Emails + phone numbers
* Unencrypted files

**Result:** You fix the issue and enforce encryption + access policies.

---

## 🛡️ **6. AWS GuardDuty – Threat Detection**

### **Purpose:**

Machine-learning based threat detection.

### **Detects:**

* Malicious IP communication
* Crypto-mining malware
* Unusual IAM activity
* Suspicious S3 access
* EC2 compromised behavior

### **Example:**

GuardDuty alerts:

> EC2 instance communicating with a known crypto-mining IP.

You investigate → find that an engineer exposed SSH port 22 publicly and the server was compromised.

**Result:** Rotate keys → Patch EC2 → Restrict SG.

---

## 🔍 **7. AWS Inspector – Vulnerability Scanner**

### **Purpose:**

Scan workloads for security vulnerabilities.

### **Scans:**

* EC2 instances (software CVEs)
* Container images (ECR)
* Lambda functions

### **Example:**

Your CI/CD pipeline pushes Docker images to ECR.
Inspector scans image → finds:

* Critical CVE in openssl
* Medium CVE in nginx version

Pipeline blocks deployment → you upgrade base image → upload again → clean scan.

---

## 👥 **8. AWS Cognito – User Authentication for Applications**

### **Purpose:**

Amazon Cognito is an AWS service that provides user sign-up, sign-in, and access control for web & mobile apps, handling authentication, authorization and user management securely and at scale.

It offers two main components:
1. **User Pools** : a user directory for sign-up/sign-in
2. **Identity Pools** : granting temporary AWS Credentials

> Cognito supports social logins (Google, Facebook) and enterprise providers (SAML, OIDC) while enabling features like MFA and custom user flows.

### **Features:**

* Signup/Login
* MFA
* Social logins (Google, Facebook)
* JWT token-based auth
* User pools + Identity pools

### **Example:**

You create:

* **Cognito User Pool:** app users
* **Cognito Hosted UI:** signup/login
* **Cognito Identity Pool:** access temporary S3 permissions

**Result:** You build authentication without coding your own backend auth.

---

## 🔐 **9. AWS CloudHSM – Hardware Security Module**

### **Purpose:**

Dedicated, single-tenant HSM for cryptographic operations.

AWS CloudHSM is a managed service providing dedicated Hardware Security Modules (HSMs) in the cloud for securely **generating**, **storing**, and **managing cryptographic keys**, helping meet strict compliance (FIPS 140-2 Level 3/FIPS 140-3 Level 3) with single-tenant access and full key control, complementing services like AWS KMS for applications needing hardware-backed key security.

### **Use cases:**

* Protecting SSL/TLS keys for web applications.
* Encrypting databases (e.g., Amazon RDS for Oracle with TDE, Amazon Redshift).
* Securing digital certificates and signing applications.
* Meeting specific key management requirements for sensitive workloads migrating to the cloud. 

### **Example:**

A bank needs PCI-DSS compliant key storage. <br>
They deploy **CloudHSM cluster** → Encrypt credit card data using custom algorithms.

**Difference from KMS:** <br>
KMS = managed, multi-tenant, simpler. <br>
CloudHSM = dedicated, stricter compliance, full control.

---

## 🔥 **10. AWS Firewall Manager – Central Policy Management**

### **Purpose:**

Manage security policies across multi-account AWS Organizations.

### **Controls:**

* WAF rules
* Shield Advanced protection
* Security Groups
* VPC firewall policies

### **Example:**

Your company has 60 AWS accounts:

* Dev
* QA
* Prod
* Analytics
* Clients

You want a rule:

❌ **No security group should allow 0.0.0.0/0 SSH**

Using Firewall Manager:

* Create SG policy
* Apply to Org Root
* Auto-remediation enabled

**Result:** Any account that adds open SSH → automatically removed.

---

## 🧩 **How These Services Work Together (Architecture View)**

| Layer                        | AWS Service                   | Purpose                                        |
| ---------------------------- | ----------------------------- | ---------------------------------------------- |
| **Identity Security**        | IAM, Cognito                  | Who can access resources & user authentication |
| **Data Security**            | KMS, CloudHSM, Macie          | Encrypt data + find sensitive data             |
| **Network Security**         | WAF, Shield, Firewall Manager | Protect against web and DDoS attacks           |
| **Threat Detection**         | GuardDuty                     | Detect suspicious behavior                     |
| **Vulnerability Management** | Inspector                     | Find and fix system/app vulnerabilities        |

---
