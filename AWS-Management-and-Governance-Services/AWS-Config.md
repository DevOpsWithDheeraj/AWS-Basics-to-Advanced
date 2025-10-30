# ⚙️ **AWS Config — Resource Configuration Tracking and Compliance**

---

## 🧠 1. **What is AWS Config?**

**AWS Config** is a **management and governance service** that **tracks, records, and evaluates the configuration** of your AWS resources.

It helps you **understand how your resources are configured**, **monitor changes over time**, and **check compliance** with your organization’s policies or best practices.

> 💡 In simple terms:
> **CloudTrail tells you *who did what***
> **AWS Config tells you *what changed and when***.

---

## 🎯 2. **Purpose**

AWS Config is used for:

* **Configuration tracking** — see the historical state of any resource.
* **Change detection** — detect configuration drifts or unauthorized changes.
* **Compliance auditing** — check if resources meet internal or industry policies.
* **Security governance** — ensure configurations align with security standards.

---

## 🧩 3. **Key Components**

| **Component**               | **Description**                                                                |
| --------------------------- | ------------------------------------------------------------------------------ |
| **Configuration Item (CI)** | Snapshot of a resource’s configuration at a point in time.                     |
| **Configuration Recorder**  | Records changes in configurations of selected resources.                       |
| **Delivery Channel**        | Delivers recorded configuration data to an S3 bucket or SNS topic.             |
| **Config Rules**            | Define compliance checks (AWS managed or custom).                              |
| **Conformance Packs**       | Group of Config Rules for a specific compliance standard (e.g., PCI-DSS, CIS). |
| **Aggregator**              | Combines data from multiple accounts and regions for centralized visibility.   |

---

## 🪜 4. **How AWS Config Works**

1. **Configuration Recorder:**
   You enable AWS Config and select which resource types to record (e.g., EC2, S3, IAM).

2. **AWS Config captures configurations:**
   Whenever a resource is created, modified, or deleted, Config records a **Configuration Item**.

3. **Data storage:**
   The configuration history is stored in an **S3 bucket** you specify.

4. **Compliance Evaluation:**
   Config evaluates resources against **Config Rules** to determine whether they comply with defined policies.

5. **Alerts and Actions:**
   Non-compliant resources can trigger **SNS notifications**, **AWS Lambda remediations**, or **Security Hub alerts**.

---

## 🧱 5. **Example 1: S3 Public Access Rule**

### 🎯 Goal:

Ensure no S3 bucket in your account is publicly accessible.

### ⚙️ Steps:

1. Create a **Managed Rule**:
   `s3-bucket-public-read-prohibited`

2. AWS Config continuously checks all S3 buckets.

3. If any bucket allows `PublicRead` or `PublicReadWrite`, it marks it as **Non-Compliant**.

4. Optionally, trigger a **Lambda function** to automatically remove the public access.

📘 **Outcome:**
Your S3 buckets stay private automatically — maintaining compliance with security policies.

---

## 🧱 **Example 2: EC2 Instance Type Compliance**

### 🎯 Goal:

Ensure only `t2.micro` and `t3.micro` instances are used in development accounts.

### ⚙️ Steps:

1. Create a **Custom AWS Config Rule** with AWS Lambda.
   The Lambda checks each EC2 instance’s type.

2. If a developer launches a larger instance (e.g., `m5.large`), Config marks it as **Non-Compliant**.

📘 **Outcome:**
You control cost and resource standardization across environments.

---

## 🧱 **Example 3: Track Security Group Changes**

### 🎯 Goal:

Monitor when security groups are modified to allow open access (0.0.0.0/0).

### ⚙️ Steps:

1. AWS Config records all changes to security group rules.
2. You can view a **timeline** of all modifications:

   * Who added the rule (via CloudTrail)
   * When it was added
   * What the previous and current states were

📘 **Outcome:**
You can detect security misconfigurations and roll back to a previous secure state.

---

## 🧱 **Example 4: Compliance Dashboard**

You can use **AWS Config Dashboard** to:

* View compliant vs non-compliant resources.
* Filter by region or account.
* Drill down into **why** a resource is non-compliant.

📘 **Example Use:**
In Infosys DevOps projects, you can ensure all resources follow:

* Encryption at rest (EBS, S3)
* IAM password policies
* No untagged resources (for billing tracking)

---

## 🔒 6. **Conformance Packs**

AWS provides **predefined compliance packs** that bundle multiple Config Rules for industry standards like:

* **CIS AWS Foundations Benchmark**
* **PCI-DSS**
* **NIST 800-53**
* **HIPAA**

📘 **Example:**
You can apply the **CIS Benchmark Pack** to your AWS account.
It automatically checks:

* Root account has MFA enabled
* CloudTrail is enabled
* Public access to S3 is blocked

✅ Helps maintain **audit readiness** for enterprise compliance.

---

## 🧠 7. **Integration with Other AWS Services**

| **Service**           | **Integration Purpose**                                   |
| --------------------- | --------------------------------------------------------- |
| **CloudTrail**        | Identify *who* made the configuration change.             |
| **SNS**               | Send notifications when a resource becomes non-compliant. |
| **Lambda**            | Automatically fix non-compliant resources.                |
| **Security Hub**      | Aggregate compliance findings.                            |
| **AWS Organizations** | Centralize Config data across multiple accounts.          |

---

## 🛠️ 8. **Benefits of AWS Config**

| **Benefit**                         | **Description**                                          |
| ----------------------------------- | -------------------------------------------------------- |
| **Continuous Monitoring**           | Tracks resource configurations and changes in real time. |
| **Compliance Automation**           | Automatically checks and remediates policy violations.   |
| **Change History**                  | View historical configurations for auditing.             |
| **Multi-Account View**              | Aggregate data across accounts and regions.              |
| **Integration with Security Tools** | Works seamlessly with GuardDuty, Security Hub, etc.      |
| **Auditing & Reporting**            | Helps with SOC2, PCI, ISO, or CIS compliance audits.     |

---

## 🧾 9. **Summary Table**

| **Feature**                   | **Description**                          | **Example Use Case**                  |
| ----------------------------- | ---------------------------------------- | ------------------------------------- |
| **Configuration Tracking**    | Records AWS resource configurations      | Track changes to security groups      |
| **Compliance Rules**          | Evaluate configurations against policies | Check if S3 buckets are public        |
| **Conformance Packs**         | Bundle of managed rules for standards    | Apply CIS AWS Benchmark               |
| **Drift Detection**           | Detect manual changes from baseline      | Detect unapproved config updates      |
| **Integration with Lambda**   | Automate remediation                     | Auto-remove public access on S3       |
| **Multi-Account Aggregation** | Central view for all AWS accounts        | Enterprise-level compliance dashboard |

---

## 🚀 10. **Real-World DevOps Use Case (Infosys Scenario)**

As a **DevOps Engineer at Infosys**, you manage multiple AWS accounts for different clients.
You use AWS Config to:

* Ensure **IAM roles** have **least privilege**.
* Verify **EBS volumes** are **encrypted**.
* Automatically **remediate public S3 buckets** using **Lambda**.
* Aggregate all results in a **central AWS Config dashboard** for the compliance team.

✅ **Result:**
You maintain **security consistency**, **audit readiness**, and **operational visibility** across all environments — **without manual checks**.

---

## 🧩 11. **AWS Config vs CloudTrail vs CloudWatch**

| **Service**    | **Focus Area** | **What It Tracks**                | **Example**               |
| -------------- | -------------- | --------------------------------- | ------------------------- |
| **CloudTrail** | Auditing       | *Who did what*                    | User deleted an S3 bucket |
| **AWS Config** | Compliance     | *What changed and is it allowed?* | S3 bucket became public   |
| **CloudWatch** | Monitoring     | *How the system is performing*    | EC2 CPU > 80%             |

---
