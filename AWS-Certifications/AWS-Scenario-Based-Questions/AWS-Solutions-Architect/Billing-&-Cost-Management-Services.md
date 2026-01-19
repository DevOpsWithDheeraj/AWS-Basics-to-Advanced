
## 1. Cost Allocation by Team

A company runs multiple applications in a single AWS account. Management wants to track AWS costs separately for each team and generate monthly reports.

**Which solution meets this requirement with the LEAST operational overhead?**

A. Create separate AWS accounts for each team <br>
B. Enable AWS Cost Explorer only <br>
C. Use AWS Cost Allocation Tags and Cost Explorer <br>
D. Enable AWS Trusted Advisor <br>

✅ **Correct Answer: C**

### Explanation:

* **Cost Allocation Tags** allow you to tag AWS resources (e.g., `Team=Dev`, `Team=QA`) and track costs by tag.
* **AWS Cost Explorer** visualizes and reports these tagged costs.
* Trusted Advisor provides recommendations, not cost breakdowns.
* Multiple accounts increase complexity and are unnecessary here.

---

## 2. Unexpected Monthly Bill Increase

An organization notices a sudden increase in its AWS monthly bill and wants to be alerted automatically when costs exceed a specific threshold.

**Which AWS service should be used?**

A. AWS Budgets <br>
B. AWS Cost Explorer <br>
C. AWS Billing Dashboard <br>
D. AWS Trusted Advisor <br>

✅ **Correct Answer: A**

### Explanation:

* **AWS Budgets** allows you to set **cost and usage thresholds** and sends alerts via email or SNS.
* Cost Explorer is for analysis, not alerts.
* Billing Dashboard shows current usage but does not send alerts.

---

## 3. Reserved Instance Purchase Decision

A workload runs continuously on EC2 instances and is expected to run for the next 2 years. The architect wants to minimize costs.

**What is the MOST cost-effective pricing option?**

A. On-Demand Instances <br>
B. Spot Instances <br>
C. 1-year Standard Reserved Instances <br>
D. 3-year Standard Reserved Instances <br>

✅ **Correct Answer: D**

### Explanation:

* **3-year Standard Reserved Instances** provide the **maximum discount (up to ~72%)** for long-term steady workloads.
* Spot Instances are not guaranteed.
* On-Demand is the most expensive option long term.

---

## 4. Centralized Billing for Multiple Accounts

A company uses multiple AWS accounts and wants a **single consolidated bill** while still tracking costs per account.

**Which AWS feature should be used?**

A. AWS Budgets <br>
B. AWS Organizations with Consolidated Billing <br>
C. AWS Cost Explorer <br>
D. AWS Control Tower <br>

✅ **Correct Answer: B**

### Explanation:

* **AWS Organizations – Consolidated Billing** provides:

  * One bill for all accounts
  * Cost visibility per account
  * Shared Reserved Instance and Savings Plan discounts
* Control Tower helps with account governance, not billing.

---

## 5. Predicting Future AWS Costs

A finance team wants to forecast AWS spending for the next 3 months based on historical usage.

**Which AWS tool should be used?**

A. AWS Budgets <br>
B. AWS Pricing Calculator <br>
C. AWS Cost Explorer <br>
D. AWS Trusted Advisor <br>

✅ **Correct Answer: C**

### Explanation:

* **AWS Cost Explorer** provides **forecasting** based on historical data.
* Pricing Calculator is used for estimating new workloads, not existing usage.
* Budgets trigger alerts but do not forecast automatically.

---

## 6. Controlling Excessive Spending by Developers

A Solutions Architect wants to prevent developers from launching expensive EC2 instance types.

**Which solution is MOST appropriate?**

A. Use AWS Budgets only <br>
B. Use AWS Cost Explorer <br>
C. Apply IAM policies with EC2 instance restrictions <br>
D. Enable Consolidated Billing <br>

✅ **Correct Answer: C**

### Explanation:

* **IAM policies** can restrict allowed EC2 instance types.
* Budgets alert after spending occurs, not before.
* This is a **preventive control**, which is preferred in architecture design.

---

## 7. Identifying Idle Resources

An architect wants recommendations to reduce costs by identifying underutilized or idle AWS resources.

**Which AWS service provides this?**

A. AWS Cost Explorer <br>
B. AWS Budgets <br>
C. AWS Trusted Advisor <br>
D. AWS Pricing Calculator <br>

✅ **Correct Answer: C**

### Explanation:

* **AWS Trusted Advisor** checks for:

  * Idle EC2 instances
  * Unused EBS volumes
  * Low utilization resources
* Cost Explorer only shows spending trends.

---

## 8. Estimating Cost Before Deployment

A startup wants to estimate the monthly AWS cost **before** launching a new architecture.

**Which AWS tool should be used?**

A. AWS Cost Explorer <br>
B. AWS Pricing Calculator <br>
C. AWS Budgets <br>
D. AWS Billing Dashboard <br>

✅ **Correct Answer: B**

### Explanation:

* **AWS Pricing Calculator** is designed to estimate costs **before deployment**.
* Cost Explorer works only after resources exist.

---

## 9. Sharing Reserved Instance Discounts

A company has multiple AWS accounts under AWS Organizations. One account purchases Reserved Instances.

**What happens to the RI discount?**

A. Discount applies only to the purchasing account <br>
B. Discount is shared across all accounts in the organization <br>
C. Discount is shared only within the same region <br>
D. Discount is lost if unused <br>

✅ **Correct Answer: B**

### Explanation:

* With **Consolidated Billing**, Reserved Instance discounts are **shared across all linked accounts**.
* This improves overall cost efficiency.

---

## 10. Granular Cost Visibility by Application

A company wants to see AWS costs grouped by application name.

**Which approach should be used?**

A. Enable detailed billing reports only <br>
B. Use AWS Budgets <br>
C. Use Cost Allocation Tags like `Application=App1` <br>
D. Use multiple VPCs <br>

✅ **Correct Answer: C**

### Explanation:

* **Cost Allocation Tags** allow grouping costs by custom dimensions like application name.
* This is the standard AWS-recommended approach.

---

### 📌 Exam Tip for SAA-Associate

Focus on:

* **Cost Allocation Tags**
* **AWS Budgets vs Cost Explorer**
* **Consolidated Billing benefits**
* **Preventive controls using IAM**
* **Choosing the most cost-effective pricing model**

---
