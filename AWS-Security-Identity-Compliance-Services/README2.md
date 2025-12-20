
# 🔐 AWS Security, Identity & Compliance – Continued

---

## 🔑 **11. AWS IAM Identity Center (SSO)**

*(Previously AWS Single Sign-On)*

### **Purpose:**

Centralized **workforce identity management** for AWS accounts and applications.

AWS IAM Identity Center (formerly AWS Single Sign-On) is a cloud service that centrally manages **workforce access** to multiple AWS accounts and applications. It is the recommended "front door" for workforce users to access AWS resources securely and efficiently

### **What it provides:**

* Single Sign-On (SSO) for:

  * AWS accounts
  * AWS console
  * CLI
  * Third-party apps (Jira, GitHub, etc.)
* Integrates with:

  * Active Directory
  * External IdPs (Azure AD, Okta)
* Permission sets instead of IAM roles per account

### **Example:**

Your company has **50 AWS accounts**.

Without Identity Center:

* Separate IAM users in each account ❌

With Identity Center:

* One corporate login (email + MFA)
* Assign:

  * **Dev team → ReadOnly in Prod**
  * **Dev team → Admin in Dev**
* Access all accounts from **one portal**

**Result:**
Centralized access control + no IAM user sprawl.

---

## 🔗 **12. AWS Resource Access Manager (RAM)**

### **Purpose:**

**Securely share AWS resources** across accounts without duplication.

### **Shareable resources:**

* VPC subnets
* Transit Gateways
* Route 53 Resolver rules
* License Manager configs

### **Example:**

Your org has:

* **Networking Account** → owns VPC
* **App Accounts** → run EC2/EKS

Instead of creating VPCs everywhere:

* Share **subnets** using RAM
* App accounts launch EC2 into shared VPC

**Result:**
Central networking + reduced cost + consistent security.

---

## 🔐 **13. AWS Secrets Manager**

### **Purpose:**

Securely **store, rotate, and access secrets**.

### **Stores:**

* Database passwords
* API keys
* OAuth tokens
* App secrets

### **Features:**

* Automatic secret rotation
* Encryption using KMS
* IAM-based access control
* Native integration with RDS, Lambda, EKS

### **Example:**

Your app connects to RDS.

❌ Hardcoded DB password in code
✅ Use Secrets Manager:

* Store DB creds
* Lambda fetches secret at runtime
* Rotation enabled every 30 days

**Result:**
No secrets in code or GitHub.

---

## 🧠 **14. AWS Security Hub**

### **Purpose:**

**Central security posture management** across AWS accounts.

### **Collects findings from:**

* GuardDuty
* Inspector
* Macie
* IAM Access Analyzer
* Third-party tools

### **Standards supported:**

* CIS AWS Foundations
* PCI-DSS
* AWS Foundational Security Best Practices

### **Example:**

Security Hub reports:

* ❌ S3 bucket public
* ❌ Root account without MFA
* ❌ Unencrypted EBS volumes

You prioritize **critical findings** and auto-remediate using Lambda.

**Result:**
One dashboard → complete security visibility.

---

## 📜 **15. AWS Artifact**

### **Purpose:**

Self-service access to **AWS compliance reports & agreements**.

### **Provides:**

* SOC reports
* ISO certifications
* PCI compliance docs
* GDPR, HIPAA agreements

### **Example:**

Your client asks:

> “Is AWS ISO 27001 compliant?”

You go to **AWS Artifact → Download ISO certificate** → Share with client.

**Result:**
Audit-ready compliance proof.

---

## 🧾 **16. AWS Audit Manager**

### **Purpose:**

Automates **evidence collection for audits**.

### **Helps with:**

* SOC 2
* ISO 27001
* PCI-DSS
* Internal security audits

### **Example:**

Preparing for SOC 2 audit:

Audit Manager automatically collects:

* CloudTrail logs
* IAM policies
* Encryption settings
* Security Group rules

Instead of manual screenshots ❌

**Result:**
Faster audits + less human error.

---

## 🔐 **17. AWS Certificate Manager (ACM)**

### **Purpose:**

Provision and manage **SSL/TLS certificates**.

### **Used with:**

* ALB
* CloudFront
* API Gateway
* Elastic Beanstalk

### **Features:**

* Free public certificates
* Auto-renewal
* Private CA support

### **Example:**

Your website uses HTTPS.

* Request certificate in ACM
* Attach to ALB
* Enable HTTPS

No manual renewal ever.

**Result:**
Secure traffic + zero certificate headaches.

---

## 🕵️ **18. Amazon Detective**

### **Purpose:**

Investigate **security incidents using graphs & timelines**.

### **Works with:**

* GuardDuty
* VPC Flow Logs
* CloudTrail

### **Example:**

GuardDuty reports suspicious activity.

Detective shows:

* Which EC2 instance
* Which IAM role
* Which IP address
* What happened before & after

**Result:**
Faster root cause analysis.

---

## 🏢 **19. AWS Directory Service**

### **Purpose:**

Managed **Active Directory in AWS**.

### **Types:**

1. **AWS Managed Microsoft AD**
2. **AD Connector** (connect to on-prem AD)
3. **Simple AD**

### **Use cases:**

* Windows EC2 login
* RDS SQL Server auth
* SSO for AWS apps

### **Example:**

Your org already uses on-prem AD.

* Use **AD Connector**
* Employees login to AWS resources using same credentials

**Result:**
No duplicate identities.

---

## 🧩 **Complete Security Architecture Map**

| Layer                   | AWS Services                           |
| ----------------------- | -------------------------------------- |
| **Workforce Identity**  | IAM Identity Center, Directory Service |
| **Access Control**      | IAM, RAM                               |
| **Secrets & Keys**      | Secrets Manager, KMS, CloudHSM         |
| **App/User Auth**       | Cognito                                |
| **Network Protection**  | WAF, Shield, Firewall Manager          |
| **Threat Detection**    | GuardDuty, Detective                   |
| **Vulnerability Mgmt**  | Inspector                              |
| **Security Posture**    | Security Hub                           |
| **Compliance & Audits** | Artifact, Audit Manager                |
| **Encryption & TLS**    | ACM                                    |

---

