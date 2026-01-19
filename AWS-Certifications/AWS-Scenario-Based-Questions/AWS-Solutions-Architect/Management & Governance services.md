
## **1. Monitoring Application Health**

A company runs a three-tier application on Amazon EC2 instances behind an Application Load Balancer. The operations team wants **real-time monitoring** of CPU utilization, request count, and to receive alerts when thresholds are breached.

**Which AWS service should be used?**

A. AWS CloudTrail <br>
B. Amazon CloudWatch <br>
C. AWS Config <br>
D. AWS Trusted Advisor <br>

✅ **Correct Answer:** **B. Amazon CloudWatch**

**Explanation:**
Amazon CloudWatch provides metrics, logs, dashboards, and alarms for AWS resources such as EC2, ALB, and RDS. CloudTrail is for API activity, Config tracks resource changes, and Trusted Advisor gives best-practice recommendations.

---

## **2. Auditing API Activity**

A security team needs to **track who made changes to AWS resources**, including the source IP address and the time of the request, for compliance audits.

**Which service meets this requirement?**

A. AWS Config <br>
B. Amazon CloudWatch Logs <br>
C. AWS CloudTrail <br>
D. AWS Systems Manager <br>

✅ **Correct Answer:** **C. AWS CloudTrail**

**Explanation:**
AWS CloudTrail records AWS API calls, including the identity of the caller, time, and IP address. It is essential for governance, compliance, and auditing.

---

## **3. Enforcing Configuration Compliance**

A company wants to ensure that **all EC2 instances use approved instance types**. Any non-compliant resource should be flagged automatically.

**Which service should be used?**

A. AWS CloudTrail <br>
B. AWS Config <br>
C. Amazon CloudWatch <br>
D. AWS Organizations <br>

✅ **Correct Answer:** **B. AWS Config**

**Explanation:**
AWS Config tracks resource configurations and evaluates them against rules to check compliance. It is ideal for detecting non-approved instance types.

---

## **4. Managing Multiple AWS Accounts**

A large enterprise has multiple AWS accounts for development, testing, and production. They want **centralized billing and policy management**.

**Which service should they use?**

A. AWS Control Tower <br>
B. AWS Systems Manager <br>
C. AWS Organizations <br>
D. AWS Trusted Advisor <br>

✅ **Correct Answer:** **C. AWS Organizations**

**Explanation:**
AWS Organizations allows centralized account management, consolidated billing, and Service Control Policies (SCPs). Control Tower builds on Organizations but is not required for basic centralized management.

---

## **5. Automating Operational Tasks**

An operations team wants to **automate patching of EC2 instances**, run commands remotely, and manage inventories without SSH access.

**Which AWS service should they use?**

A. AWS CloudFormation <br>
B. AWS Systems Manager <br>
C. Amazon CloudWatch <br>
D. AWS OpsWorks <br>

✅ **Correct Answer:** **B. AWS Systems Manager**

**Explanation:**
AWS Systems Manager provides automation, patch management, run command, and inventory features without requiring direct instance access.

---

## **6. Tracking Cost Optimization Opportunities**

A company wants **recommendations to reduce costs**, improve performance, and increase security across AWS resources.

**Which service provides these recommendations?**

A. AWS Budgets <br>
B. AWS Cost Explorer <br>
C. AWS Trusted Advisor <br>
D. AWS Config <br>

✅ **Correct Answer:** **C. AWS Trusted Advisor**

**Explanation:**
AWS Trusted Advisor checks AWS environments against best practices for cost optimization, performance, security, fault tolerance, and service limits.

---

## **7. Infrastructure as Code Governance**

A solutions architect wants to **standardize infrastructure deployments** and ensure repeatability using templates.

**Which service should be used?**

A. AWS Elastic Beanstalk <br>
B. AWS CloudFormation <br>
C. AWS Systems Manager <br>
D. AWS Config <br>

✅ **Correct Answer:** **B. AWS CloudFormation**

**Explanation:**
AWS CloudFormation enables Infrastructure as Code (IaC) using templates to provision and manage AWS resources in a consistent and controlled manner.

---

## **8. Logging Application Events Centrally**

A company wants to **collect, store, and analyze logs** from EC2 instances and AWS Lambda functions centrally.

**Which service should be used?**

A. AWS CloudTrail <br>
B. Amazon CloudWatch Logs <br>
C. AWS Config <br>
D. AWS X-Ray <br>

✅ **Correct Answer:** **B. Amazon CloudWatch Logs**

**Explanation:**
CloudWatch Logs stores and analyzes log data from AWS services and applications. X-Ray is for tracing requests, not log storage.

---

## **9. Preventing Accidental Resource Deletion**

A company wants to **restrict users from deleting critical resources**, even if they have IAM permissions.

**Which AWS feature should be used?**

A. IAM Roles <br>
B. Resource-based policies <br>
C. Service Control Policies (SCPs) <br>
D. AWS Config Rules <br>

✅ **Correct Answer:** **C. Service Control Policies (SCPs)**

**Explanation:**
SCPs in AWS Organizations define maximum permissions for accounts and can prevent actions like deletion, regardless of IAM permissions.

---

## **10. Setting Up an Account Governance Baseline**

A company wants to quickly set up **secure, multi-account governance with best practices**, including logging and account structure.

**Which service should be used?**

A. AWS Organizations <br>
B. AWS Control Tower <br>
C. AWS Systems Manager <br>
D. AWS Config <br>

✅ **Correct Answer:** **B. AWS Control Tower**

**Explanation:**
AWS Control Tower provides an automated way to set up and govern a multi-account AWS environment with built-in best practices, guardrails, and centralized logging.

---

### ✅ **Exam Tip for SAA**

* **CloudWatch** → Monitoring & alerts
* **CloudTrail** → API activity & audit
* **AWS Config** → Configuration compliance
* **Systems Manager** → Operations & automation
* **Organizations & SCPs** → Multi-account governance
* **Control Tower** → Account factory & guardrails

---
