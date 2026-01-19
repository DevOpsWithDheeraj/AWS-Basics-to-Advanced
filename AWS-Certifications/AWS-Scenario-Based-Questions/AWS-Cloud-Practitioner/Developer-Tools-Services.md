
## **1. Continuous Integration Setup**

A development team wants to automatically build and test their code every time a developer pushes code to a Git repository hosted on AWS.

**Which AWS service should they use?**

A. AWS CodeDeploy <br>
B. AWS CodeBuild <br>
C. AWS CodePipeline <br>
D. AWS CloudFormation <br>

✅ **Correct Answer:** **B. AWS CodeBuild**

**Explanation:**
AWS CodeBuild is a fully managed **build and test service** that compiles source code, runs tests, and produces artifacts automatically when code is pushed.

---

## **2. End-to-End CI/CD Automation**

A company wants to automate the entire process of source, build, test, and deploy stages for their application.

**Which AWS service orchestrates this workflow?**

A. AWS CodeCommit <br>
B. AWS CodePipeline <br>
C. AWS CodeDeploy <br>
D. AWS Elastic Beanstalk <br>

✅ **Correct Answer:** **B. AWS CodePipeline**

**Explanation:**
AWS CodePipeline automates and coordinates **all phases of CI/CD**, integrating with CodeCommit, CodeBuild, and CodeDeploy.

---

## **3. Secure Git Repository on AWS**

A team wants a **private, secure Git-based repository** managed entirely by AWS without using third-party tools.

**Which service should they choose?**

A. GitHub <br>
B. AWS CodeArtifact <br>
C. AWS CodeCommit <br>
D. AWS CodeDeploy <br>

✅ **Correct Answer:** **C. AWS CodeCommit**

**Explanation:**
AWS CodeCommit is a **fully managed Git repository service** with encryption, access control, and high availability.

---

## **4. Automated Application Deployment**

An application needs to be automatically deployed to **EC2 instances** with minimal downtime.

**Which AWS service handles this requirement?**

A. AWS CodePipeline <br>
B. AWS CodeBuild <br>
C. AWS CodeDeploy <br>
D. AWS OpsWorks <br>

✅ **Correct Answer:** **C. AWS CodeDeploy**

**Explanation:**
AWS CodeDeploy automates **application deployments** to EC2, Lambda, and on-premises servers with deployment strategies like rolling updates.

---

## **5. Artifact Management for Developers**

Developers want a **central repository to store and manage software packages** (like Maven, npm, or Python packages).

**Which AWS service fits this use case?**

A. AWS CodeCommit <br>
B. AWS CodeBuild <br>
C. AWS CodeArtifact <br>
D. AWS CodePipeline <br>

✅ **Correct Answer:** **C. AWS CodeArtifact**

**Explanation:**
AWS CodeArtifact is a **fully managed artifact repository service** that securely stores and shares packages.

---

## **6. Serverless CI/CD for Lambda Functions**

A company wants to deploy **AWS Lambda functions automatically** when new code is committed.

**Which combination of services is MOST appropriate?**

A. CodeCommit + CodeBuild + CodeDeploy <br>
B. CodeCommit + CodePipeline + CodeDeploy <br>
C. CodePipeline only <br>
D. CloudFormation only <br>

✅ **Correct Answer:** **B. CodeCommit + CodePipeline + CodeDeploy**

**Explanation:**
This combination provides **source control, pipeline orchestration, and automated Lambda deployments**, which is a common CI/CD pattern.

---

## **7. Pay-as-You-Go Build Service**

A startup wants to avoid managing build servers and only pay when builds are running.

**Which AWS service meets this requirement?**

A. AWS CodePipeline <br>
B. AWS CodeBuild <br>
C. AWS EC2 <br>
D. AWS CodeDeploy <br>

✅ **Correct Answer:** **B. AWS CodeBuild**

**Explanation:**
CodeBuild is **serverless** and charged **per build minute**, eliminating infrastructure management.

---

## **8. Visual CI/CD Workflow**

Which AWS Developer Tool provides a **visual representation** of the CI/CD process?

A. AWS CodeBuild <br>
B. AWS CodeCommit <br>
C. AWS CodePipeline <br>
D. AWS CodeDeploy <br>

✅ **Correct Answer:** **C. AWS CodePipeline**

**Explanation:**
CodePipeline shows stages like **Source → Build → Test → Deploy** in a visual workflow, making it easy to monitor progress.

---

## **9. Deployment Strategy with Minimal Risk**

Which AWS service supports **blue/green deployments** to reduce application downtime?

A. AWS CodeBuild <br>
B. AWS CodePipeline <br>
C. AWS CodeCommit <br>
D. AWS CodeDeploy <br>

✅ **Correct Answer:** **D. AWS CodeDeploy**

**Explanation:**
CodeDeploy supports **blue/green and rolling deployments**, helping reduce deployment risk and downtime.

---

## **10. Exam Tip Question**

Which statement BEST describes AWS Developer Tools?

A. They are mainly used for monitoring infrastructure <br>
B. They help automate software development and deployment <br>
C. They are used only for server management <br>
D. They replace AWS security services <br>

✅ **Correct Answer:** **B. They help automate software development and deployment**

**Explanation:**
AWS Developer Tools focus on **CI/CD, source control, builds, testing, and deployment automation**.

---

### ✅ **Cloud Practitioner Exam Tip**

You should **recognize service purposes**, not deep configuration:

* **CodeCommit** → Source control
* **CodeBuild** → Build & test
* **CodeDeploy** → Deploy
* **CodePipeline** → Orchestrate CI/CD
* **CodeArtifact** → Package repository

---
