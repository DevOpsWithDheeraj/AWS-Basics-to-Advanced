
## 1. Continuous Integration for Microservices

**Scenario:**
A company has multiple microservices stored in separate Git repositories. Every code commit must automatically trigger a build, run unit tests, and store build artifacts securely.

**Which AWS solution best meets this requirement?**

A. AWS CodeCommit + AWS CodeDeploy <br>
B. AWS CodeCommit + AWS CodeBuild + Amazon S3 <br>
C. AWS CodePipeline + AWS CodeDeploy <br>
D. AWS CodeBuild + AWS Elastic Beanstalk <br>

✅ **Correct Answer: B**

**Explanation:**

* **CodeCommit** stores the source code
* **CodeBuild** runs builds and unit tests
* **Amazon S3** stores build artifacts
* CodePipeline is optional and not required for simple CI
  This combination is commonly tested in SAA for CI workflows.

---

## 2. Fully Managed CI/CD with Minimal Administration

**Scenario:**
A startup wants a **fully managed CI/CD pipeline** that automatically pulls code from a repository, builds it, tests it, and deploys it to production with minimal setup.

**Which AWS service should be used to orchestrate the entire workflow?**

A. AWS CodeBuild <br> 
B. AWS CodeDeploy <br>
C. AWS CodePipeline <br>
D. AWS Elastic Beanstalk <br>

✅ **Correct Answer: C**

**Explanation:**

* **CodePipeline** orchestrates CI/CD workflows
* Integrates with CodeCommit, CodeBuild, CodeDeploy, and third-party tools
* Minimal operational overhead
  CodePipeline is the *central automation service* for CI/CD.

---

## 3. Blue/Green Deployment for EC2 Instances

**Scenario:**
An application runs on Amazon EC2 instances in an Auto Scaling group. The company wants to deploy new versions with **zero downtime** and the ability to quickly roll back.

**Which AWS service supports this requirement?**

A. AWS CodeBuild <br>
B. AWS Elastic Beanstalk <br>
C. AWS CodeDeploy <br>
D. AWS CodePipeline <br>

✅ **Correct Answer: C**

**Explanation:**

* **CodeDeploy** supports **blue/green** and **rolling deployments**
* Works with EC2, Auto Scaling, Lambda, and ECS
* Allows automatic rollback on failure
  This is a classic SAA deployment question.

---

## 4. Secure Git-Based Source Control

**Scenario:**
A development team needs a **highly available, secure, Git-compatible repository** that integrates with IAM for access control.

**Which AWS service should they use?**

A. Amazon S3 <br>
B. AWS CodeCommit <br>
C. AWS CodeBuild <br>
D. AWS CodePipeline <br>

✅ **Correct Answer: B**

**Explanation:**

* **CodeCommit** is a fully managed Git repository
* Integrated with IAM for authentication and authorization
* Encrypted at rest and in transit
  SAA focuses on **security and integration**, not Git commands.

---

## 5. Serverless Application Deployment Automation

**Scenario:**
A team deploys AWS Lambda functions and wants an automated way to safely release new versions using **traffic shifting**.

**Which service should be used?**

A. AWS CodePipeline <br>
B. AWS CodeDeploy <br>
C. AWS CodeBuild <br>
D. AWS CloudFormation <br>

✅ **Correct Answer: B**

**Explanation:**

* **CodeDeploy** supports **Lambda traffic shifting** (canary, linear, all-at-once)
* Enables safe rollouts and rollback
  Often tested for serverless deployment strategies.

---

## 6. Infrastructure as Code for Repeatable Environments

**Scenario:**
An architect wants to define application infrastructure (EC2, ALB, RDS) using code so that environments can be recreated reliably.

**Which AWS service should be used?**

A. AWS CodePipeline <br>
B. AWS CodeDeploy <br>
C. AWS CloudFormation <br>
D. AWS CodeBuild <br>

✅ **Correct Answer: C**

**Explanation:**

* **CloudFormation** is Infrastructure as Code (IaC)
* Ensures repeatable and consistent environments
* Frequently appears with CI/CD questions in SAA exams.

---

## 7. Reducing Operational Overhead for Web App Deployment

**Scenario:**
A company wants developers to upload application code, and AWS should handle **provisioning, scaling, and deployment automatically**.

**Which service is best suited?**

A. AWS CodeDeploy <br>
B. AWS Elastic Beanstalk <br>
C. AWS CodeBuild <br>
D. AWS CloudFormation <br>

✅ **Correct Answer: B**

**Explanation:**

* **Elastic Beanstalk** is a PaaS service
* Handles infrastructure, load balancing, scaling, and deployment
* Often tested as a *simpler alternative* to CI/CD pipelines.

---

## 8. Automated Approval Before Production Deployment

**Scenario:**
A financial application requires **manual approval** before deploying changes to production.

**Which AWS service supports this requirement natively?**

A. AWS CodeDeploy <br>
B. AWS CodeBuild <br>
C. AWS CodePipeline <br>
D. AWS CodeCommit <br>

✅ **Correct Answer: C**

**Explanation:**

* **CodePipeline** supports **manual approval actions**
* Commonly used in regulated environments
  This tests governance and compliance knowledge.

---

## 9. Running Build Jobs Without Managing Servers

**Scenario:**
Developers need to compile code and run tests **without provisioning or managing build servers**.

**Which service should they use?**

A. Amazon EC2 <br>
B. AWS CodeBuild <br>
C. AWS CodeDeploy <br>
D. AWS Lambda <br>

✅ **Correct Answer: B**

**Explanation:**

* **CodeBuild** is fully serverless
* Automatically scales build environments
* Pay only for build time
  This is a frequent exam concept.

---

## 10. End-to-End CI/CD Architecture

**Scenario:**
A company wants an **end-to-end CI/CD solution**:

* Source control
* Build and test
* Deployment to EC2

**Which combination is BEST?**

A. CodeCommit + CodePipeline + CodeBuild + CodeDeploy  <br>
B. S3 + EC2 + Lambda <br>
C. CodeCommit + Elastic Beanstalk <br>
D. CloudFormation + OpsWorks <br>

✅ **Correct Answer: A**

**Explanation:**
This is the **canonical AWS CI/CD architecture**:

* **CodeCommit** – source
* **CodePipeline** – orchestration
* **CodeBuild** – build/test
* **CodeDeploy** – deployment
  Very high-probability SAA exam question.

---

### 🎯 Exam Tip for SAA

* Focus on **when to use which developer tool**, not syntax
* Understand **CI vs CD vs IaC**
* Expect **architecture-level decisions**, not developer-level coding

---
