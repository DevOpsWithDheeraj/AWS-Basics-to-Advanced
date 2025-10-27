# AWS Developer Tools

AWS Developer Tools provide **services for DevOps automation, CI/CD, and monitoring** to help developers build, test, deploy, and monitor applications efficiently in AWS.

---

## 🧑‍💻 **1. AWS Cloud9 — Cloud-based IDE**

**Purpose:** Cloud9 is an online IDE (Integrated Development Environment) where you can write, run, and debug code directly in your browser — no local setup needed.

**Features:**

* Supports multiple languages (Python, Java, Node.js, C++, etc.)
* Pre-configured terminal with AWS CLI.
* Great for pair programming and remote development.

**Example:**
A developer creates a Python web app in **AWS Cloud9**, writes the code, tests APIs using the built-in terminal, and pushes changes to **CodeCommit** directly — all within the browser.

---

## 📘 **2. AWS CodeCommit — Source Code Repository**

**Purpose:** CodeCommit is a fully-managed **Git-based repository** for hosting your source code privately.

**Features:**

* Similar to GitHub or Bitbucket but fully hosted on AWS.
* Integrates with IAM for fine-grained access control.
* Encrypted and scalable.

**Example:**
Your team stores application code in **CodeCommit**:

```
git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/MyAppRepo
```

Developers push their latest commits, triggering a **CodePipeline** to start a build and deployment automatically.

---

## 🔨 **3. AWS CodeBuild — Build & Test Automation**

**Purpose:** CodeBuild compiles your source code, runs tests, and produces deployable artifacts (like `.jar`, `.zip`, or Docker images).

**Features:**

* Fully managed build service (no build servers needed).
* Integrates with CodeCommit, S3, and CodePipeline.
* Pay only for the build time used.

**Example:**
When a developer commits code to CodeCommit:

1. CodePipeline triggers **CodeBuild**.
2. CodeBuild uses a `buildspec.yml` file to run commands:

   ```yaml
   version: 0.2
   phases:
     build:
       commands:
         - mvn clean package
   artifacts:
     files:
       - target/*.jar
   ```
3. The output JAR file is stored in S3 for deployment.

---

## 🔁 **4. AWS CodePipeline — CI/CD Orchestration**

**Purpose:** CodePipeline automates the **entire CI/CD process** — from source to build to test to deploy.

**Features:**

* Integrates with CodeCommit, CodeBuild, CodeDeploy, CloudFormation, and 3rd-party tools.
* Fully managed — automatically triggers on commits.
* Visual workflow view.

**Example:**
A simple pipeline:

```
Source → Build → Deploy
```

* **Source:** CodeCommit detects a commit.
* **Build:** CodeBuild compiles the app and runs tests.
* **Deploy:** CodeDeploy deploys the app to EC2 or Lambda.

This ensures **every code change** automatically goes through the CI/CD process.

---

###🚀 **5. AWS CodeDeploy — Automated Deployment**

**Purpose:** CodeDeploy automates application deployments to **EC2**, **ECS**, **Lambda**, or **on-premise servers**.

**Features:**

* Blue/Green & Rolling deployments.
* Automatic rollback on failure.
* Integrates with CodePipeline.

**Example:**
After a successful build:

* **CodeDeploy** picks up the artifact.
* It deploys a new version of your web app to EC2 instances using an `appspec.yml` file:

  ```yaml
  version: 0.0
  os: linux
  files:
    - source: /
      destination: /var/www/html
  hooks:
    AfterInstall:
      - location: scripts/restart_server.sh
  ```

This ensures zero-downtime deployment.

---

## 🔗 **Putting It All Together (Real-World Example)**

**Goal:** Deploy a web app automatically to EC2 every time code is pushed.

1. **Developer writes code** in **Cloud9**.
2. **Pushes to CodeCommit** (Source stage).
3. **CodePipeline triggers** a build.
4. **CodeBuild compiles and tests** the app.
5. **CodeDeploy deploys** it to EC2.
6. **Pipeline completes** automatically — no manual work!

---

## ✅ Summary Table

| Tool             | Purpose                 | Example Usage                     |
| ---------------- | ----------------------- | --------------------------------- |
| **Cloud9**       | Online IDE              | Write & test code in browser      |
| **CodeCommit**   | Source code repo        | Store versioned app code          |
| **CodeBuild**    | Build & test automation | Compile code & generate artifacts |
| **CodePipeline** | CI/CD orchestration     | Automate build → test → deploy    |
| **CodeDeploy**   | Deployment automation   | Deploy app to EC2, ECS, or Lambda |

---
