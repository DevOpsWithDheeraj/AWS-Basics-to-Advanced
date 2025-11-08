
# 🧩 **What is AWS Config?**

**AWS Config** is a **configuration tracking and compliance service** that helps you:

* **Track changes** to AWS resources (who changed what, and when).
* **Audit configurations** for compliance with security or governance rules.
* **Evaluate** if your AWS resources meet best practices or company policies.

Think of it as the **CCTV camera** of your AWS account — it records every configuration change.

---

## ⚙️ **How AWS Config Works**

1. **Configuration Recorder**

   * Tracks configuration changes to supported AWS resources (like EC2, S3, IAM, Security Groups, etc.).

2. **Delivery Channel**

   * Delivers configuration snapshots and history to **an S3 bucket** and **CloudWatch Events**.

3. **Rules and Evaluations**

   * You can define **AWS Config Rules** (predefined or custom) to automatically check compliance.

---

## 🧠 **Example 1: Tracking Security Group Changes**

### 🎯 Goal:

Track if someone modifies or opens a port (like port 22 for SSH) in a security group.

### 🧩 Steps:

1. **Enable AWS Config:**

   * Go to **AWS Console → AWS Config**.
   * Choose:

     * S3 bucket for storing snapshots.
     * AWS Config recorder to track all resources.
     * IAM Role for Config.

2. **AWS Config starts recording:**
   Every time someone:

   * Adds/Removes a rule in Security Group
   * Changes EC2 instance type
   * Modifies an S3 bucket policy
     → AWS Config records it.

3. **View the Configuration History:**
   You can open the AWS Config dashboard to see:

   ```
   Resource: sg-0123456
   Change: Inbound rule added (port 22, 0.0.0.0/0)
   Time: 2025-11-08 09:00 UTC
   User: admin@example.com
   ```

✅ So you can **see who changed what**, when, and restore previous configurations if needed.

---

## 🧠 **Example 2: Compliance Rule for S3 Buckets**

### 🎯 Goal:

Ensure all S3 buckets are **not publicly accessible**.

### 🧩 Steps:

1. Go to AWS Config → Rules → Add Rule

2. Choose a **Managed Rule**:

   ```
   s3-bucket-public-read-prohibited
   ```

3. Apply to all resources.

4. AWS Config scans all S3 buckets and returns:

   * **Compliant:** Private bucket
   * **Noncompliant:** Public bucket

Example Output:

| Bucket Name      | Compliance State |
| ---------------- | ---------------- |
| prod-data-bucket | ✅ Compliant      |
| test-logs-bucket | ❌ Noncompliant   |

✅ This helps maintain **security compliance automatically**.

---

## 🧠 **Example 3: Custom Rule using Lambda**

If you need custom logic — for example:

> “EC2 instances must use a specific AMI or be tagged with `Environment=Prod`”

You can create a **Custom AWS Config Rule** that runs a **Lambda function** to check compliance.

```python
# Example AWS Lambda code for Config Rule
def lambda_handler(event, context):
    configuration_item = event['configurationItem']
    tags = configuration_item['tags']
    
    if 'Environment' in tags and tags['Environment'] == 'Prod':
        compliance = 'COMPLIANT'
    else:
        compliance = 'NON_COMPLIANT'
    
    return {
        'compliance_type': compliance,
        'annotation': 'Instance must be tagged with Environment=Prod'
    }
```

---

## 🛡️ **Benefits of AWS Config**

| Feature                       | Description                                          |
| ----------------------------- | ---------------------------------------------------- |
| **Change Tracking**           | View historical changes to resources.                |
| **Compliance Monitoring**     | Evaluate resources against AWS best practices.       |
| **Integration**               | Works with CloudTrail, CloudWatch, and Security Hub. |
| **Automatic Remediation**     | Can trigger Lambda to fix noncompliant resources.    |
| **Multi-Account Aggregation** | Combine data from multiple AWS accounts.             |

---

## 🧾 **Summary**

| Aspect                | Description                                                            |
| --------------------- | ---------------------------------------------------------------------- |
| **Service Name**      | AWS Config                                                             |
| **Purpose**           | Track configuration changes and evaluate compliance                    |
| **Key Components**    | Configuration Recorder, Delivery Channel, Rules                        |
| **Integrations**      | CloudTrail, S3, Lambda                                                 |
| **Example Use Cases** | Detect public S3 buckets, track security group changes, tag compliance |
| **Pricing**           | Pay per configuration item recorded and rule evaluation                |

---

## 🔍 **In Short**

* 🧠 **AWS Config = Configuration + Compliance**
* 🕵️ **Tracks resource changes**
* ✅ **Evaluates compliance**
* 🔁 **Can auto-remediate via Lambda**

---
