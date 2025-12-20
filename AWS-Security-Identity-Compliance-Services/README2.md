
# 🔐 AWS Security, Identity & Compliance – Continued

---

## 🔑 **11. AWS IAM Identity Center (SSO)**

*(Previously AWS Single Sign-On)*

### **Purpose:**

Centralized **workforce identity management** for AWS accounts and applications.

AWS IAM Identity Center (formerly AWS Single Sign-On) is a cloud service that centrally manages **workforce access** to multiple AWS accounts and applications. <br>
It is the recommended "front door" for workforce users to access AWS resources securely and efficiently

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

* AWS Resource Access Manager (RAM) is an AWS service that lets you securely share your AWS resources (like VPCs, subnets, AMI, RDS databases) across multiple AWS accounts, either within your AWS Organization, to specific Organizational Units (OUs), or to individual accounts, enabling central management and efficient use of resources without duplication.  <br>

* It simplifies multi-account setups by allowing you to create a resource once and make it accessible to others, supporting least-privilege access through managed permissions. 

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

* AWS Secrets Manager is a managed service for securely storing, retrieving, and rotating **sensitive information** like **database credentials**, **API keys**, and **tokens**, eliminating the need to hardcode them in applications for better security and compliance. 

* It allows programmatic access to secrets, centralizes management, automates secret rotation, and integrates with AWS KMS for encryption, enhancing security posture and simplifying credential lifecycle management. 

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

### **How it Works**:
* Store: You store your secret (e.g., a password) in Secrets Manager, specifying its name and encryption settings.
* Retrieve: Your application makes an API call to Secrets Manager to fetch the secret at runtime.
* Rotate: You configure a rotation schedule, often using a Lambda function, to automatically update the secret in the service and in Secrets Manager. 

### **Example:**

Your app connects to RDS.

❌ Hardcoded DB password in code <br>
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

* AWS Security Hub is a cloud security service that gives you a unified view of your security posture across AWS, centralizing findings, prioritizing critical issues, and streamlining responses at scale by correlating data from multiple AWS security tools (like GuardDuty, Inspector, Macie) and third-party partners into actionable insights and automated workflows.

* It helps you identify, prioritize, and respond to risks faster, improving team productivity and cloud protection. 

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

### **How it Works**:
* Collects Data: Gathers findings from integrated security services and third-party tools.
* Analyzes & Enriches: Adds context (e.g., does this finding involve sensitive data?) to make it more meaningful.
* Visualizes: Presents security posture with dashboards, trends, and exposure summaries.
* Enables Action: Facilitates immediate response through insights, automation, and integrations. 

> In essence, Security Hub acts as a security command center, giving you a single pane of glass to see, understand, and manage security across your entire AWS presence. 

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

* AWS Artifact is a free, self-service portal within the AWS console that gives you on-demand access to AWS's security and compliance documentation, like SOC, PCI, and ISO reports, plus agreements (e.g., BAA) for your AWS accounts, helping you prove compliance and understand the security posture of the AWS infrastructure for your auditors and regulators. 

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

* AWS Audit Manager is a service that simplifies risk and compliance management by automating the continuous collection and organization of evidence from your AWS usage, helping you audit against industry standards (like PCI DSS, HIPAA, NIST) and internal controls with less manual effort, generating audit-ready reports with verifiable data, and providing tools for delegation and evidence sharing.

* It reduces the "all hands on deck" workload during audits by mapping AWS resources to controls and presenting them in easy-to-understand reports for auditors. 

### **Helps with:**

* SOC 2
* ISO 27001
* PCI-DSS
* Internal security audits

### **How it Works**:
* Set Up: Choose a prebuilt framework or create a custom one, defining controls relevant to your audit.
* Scope: Specify the AWS accounts and services to be included in the assessment.
* Automate: Audit Manager continuously collects evidence (logs, configurations, security findings) related to your controls.
* Review: Manage stakeholder evaluations and delegate tasks.
* Report: Generate assessment reports that bundle evidence and control summaries for auditors. 

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

* AWS Certificate Manager (ACM) is an AWS service that simplifies provisioning, managing, and deploying SSL/TLS certificates for securing network traffic on AWS and connected resources, handling public and private certificates, including automated renewals, removing manual work. 
* You request or import certificates, then deploy them to integrated services like Elastic Load Balancers (ALB), Amazon CloudFront, and API Gateway, with ACM managing renewals automatically. 

### **Used with:**

* ALB
* CloudFront
* API Gateway
* Elastic Beanstalk

### **Features:**

* Free public certificates
* Auto-renewal
* Private CA support

### **How it Works (Example with Load Balancer)**:
* Request or import an SSL/TLS certificate for your domain using ACM.
* Create an Application Load Balancer (ALB) (or other integrated service).
* Configure the ALB with an HTTPS listener and associate the ACM certificate.
* Point your domain (e.g., via Amazon Route 53) to the ALB.
* ACM automatically renews the certificate before it expires, updating the ALB. 

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

