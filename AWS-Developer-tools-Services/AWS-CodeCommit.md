# AWS CodeCommit

## What is AWS CodeCommit?

**AWS CodeCommit** is a fully managed **source control service** that hosts **Git repositories** in the AWS cloud. It allows developers to securely store and manage **source code**, **binary files**, and **application assets**.  

CodeCommit is highly scalable, integrates with other AWS DevOps services, and eliminates the need to manage your own Git servers. It supports **private repositories** with **fine-grained access control** using AWS IAM.

---

## Key Features of AWS CodeCommit

1. **Fully Managed Git Service**: No server management required; AWS handles scaling, patching, and backups.
2. **Secure**: Uses **AWS IAM** for authentication and **encryption at rest and in transit**.
3. **High Availability**: CodeCommit replicates repositories across multiple AWS regions.
4. **Integration with DevOps Tools**:
   - AWS CodePipeline
   - AWS CodeBuild
   - AWS CodeDeploy
5. **Notifications & Triggers**: Notify via SNS, Lambda, or CloudWatch on repository changes.
6. **Large File Support**: Supports large binary files with Git LFS (Large File Storage).
7. **Private Repository Access**: Fine-grained permissions using IAM policies.
8. **Branching & Merging**: Supports standard Git workflows including branching, merging, pull requests, and tags.

---

## AWS CodeCommit Architecture

1. **Repository**: A Git repository where code is stored.
2. **Branches**: Separate development streams within the repository (e.g., `main`, `dev`).
3. **Commits**: Snapshots of code changes.
4. **Pull Requests**: Used to review and merge code changes.
5. **Triggers**: Automatically trigger AWS Lambda, CodeBuild, or SNS when events occur (push, merge, tag).

**Flow**:

- Developer clones repository → makes changes → commits → pushes changes → triggers optional actions (build, deploy, notifications).

---

## Step-by-Step Guide to Configure AWS CodeCommit

### Step 1: Create a Repository

1. Go to **AWS Management Console → CodeCommit → Repositories → Create Repository**.
2. Provide:
   - **Repository Name**: e.g., `my-app-repo`
   - **Description**: Optional description
3. Click **Create Repository**.
4. Note the repository URL (HTTPS or SSH).

---

### Step 2: Set Up Local Git Environment

1. Install Git on your system:
   ```bash
   git --version

2. Configure Git username and email:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

---

### Step 3: Connect to CodeCommit

#### Option 1: HTTPS with IAM Credentials

1. Create **AWS IAM user** with `AWSCodeCommitFullAccess`.
2. Configure HTTPS Git credentials for AWS CodeCommit:

   * In IAM console → Security credentials → HTTPS Git credentials → Generate.
3. Clone repository:

   ```bash
   git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/my-app-repo
   ```
4. Enter IAM HTTPS credentials when prompted.

#### Option 2: SSH Key Authentication

1. Generate SSH key:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
2. Upload public key to IAM user → SSH keys for AWS CodeCommit.
3. Clone repository using SSH:

   ```bash
   git clone ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/my-app-repo
   ```

---

### Step 4: Make Changes and Push

1. Navigate to cloned repository:

   ```bash
   cd my-app-repo
   ```
2. Create a new file:

   ```bash
   echo "print('Hello CodeCommit')" > app.py
   ```
3. Stage and commit changes:

   ```bash
   git add app.py
   git commit -m "Initial commit"
   ```
4. Push changes:

   ```bash
   git push origin main
   ```

---

### Step 5: Create Branch and Pull Request (Optional)

1. Create a branch:

   ```bash
   git checkout -b feature/login
   ```
2. Make changes and push:

   ```bash
   git add login.py
   git commit -m "Add login feature"
   git push origin feature/login
   ```
3. In CodeCommit console → Pull requests → Create pull request from `feature/login` to `main`.
4. Review and merge changes.

---

### Step 6: Enable Triggers (Optional)

1. Go to repository → **Triggers** → **Create Trigger**.
2. Configure:

   * **Event type**: Push, Merge, Tag
   * **Target**: SNS, Lambda, CodeBuild
3. Example: Trigger a CodeBuild project on every push to `main`.

---

## Practical Example: CI/CD Integration

### Scenario

* Repository: `my-app-repo`
* CI/CD: CodePipeline + CodeBuild + CodeDeploy
* Goal: Automatically build and deploy app on every commit to `main`.

### Step 1: Create CodeCommit Repository

* Name: `my-app-repo`
* Clone locally and add source code.

### Step 2: Push Code

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### Step 3: Create CodePipeline

1. Source: AWS CodeCommit (`my-app-repo`)
2. Build: AWS CodeBuild project
3. Deploy: AWS CodeDeploy to EC2/Elastic Beanstalk
4. On commit to `main`, CodePipeline automatically builds and deploys the app.

---

## Best Practices

1. Use **branching strategies**: GitFlow, GitHub Flow, or trunk-based development.
2. Enable **multi-factor authentication (MFA)** for IAM users.
3. Set up **triggers** for CI/CD or notifications.
4. Use **pull requests** for code reviews.
5. Enable **encryption** for sensitive repositories.
6. Monitor repository activity using **CloudWatch** and **CloudTrail**.

---

## Summary

AWS CodeCommit is a **secure, scalable Git repository service** that integrates seamlessly with AWS DevOps services. It simplifies source code management, supports automated workflows, and provides high availability.

**Practical Example**: Hosting `my-app-repo` on CodeCommit and integrating it with CodePipeline and CodeBuild enables **automatic CI/CD**, improving productivity and reliability in software delivery.

---

**References**:

* [AWS CodeCommit Documentation](https://docs.aws.amazon.com/codecommit/)
* [AWS DevOps Services Overview](https://aws.amazon.com/devops/)
