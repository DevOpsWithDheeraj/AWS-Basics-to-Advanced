# AWS CodePipeline

## What is AWS CodePipeline?

**AWS CodePipeline** is a fully managed **continuous integration and continuous delivery (CI/CD) service** that automates the build, test, and deployment phases of application release processes.  

CodePipeline allows you to model the **entire software release workflow** using stages, actions, and transitions. It integrates seamlessly with AWS services like **CodeCommit**, **CodeBuild**, **CodeDeploy**, **Elastic Beanstalk**, **S3**, **ECS**, and external tools like GitHub or Jenkins.

---

## Key Features of AWS CodePipeline

1. **Automated CI/CD Workflow**: Automates code build, test, and deployment.
2. **Stages and Actions**:
   - **Stage**: Logical grouping of actions (e.g., source, build, deploy)
   - **Action**: A single task within a stage (e.g., CodeBuild build)
3. **Integration with AWS Services**:
   - **Source**: CodeCommit, GitHub, Bitbucket, S3
   - **Build**: CodeBuild, Jenkins
   - **Deploy**: CodeDeploy, Elastic Beanstalk, ECS, CloudFormation
4. **Parallel and Sequential Actions**: Supports multiple actions in a stage, sequential or parallel.
5. **Automatic Triggers**: Builds trigger on source code changes (push or commit).
6. **Customizable Workflows**: Supports manual approval actions, testing, and validation stages.
7. **Notifications & Logging**: Integration with SNS, CloudWatch, and CloudTrail.
8. **Security**: Uses IAM for fine-grained access control.

---

## AWS CodePipeline Architecture

1. **Source Stage**: Detects changes in source repository (CodeCommit, GitHub, S3).
2. **Build Stage**: Compiles and tests code (CodeBuild, Jenkins).
3. **Test Stage**: Optional stage for automated testing.
4. **Deploy Stage**: Deploys to AWS services (CodeDeploy, ECS, S3).
5. **Pipeline Execution**:
   - Trigger → Stage 1 → Stage 2 → … → Stage N → Completion
6. **Artifacts**: Input/output artifacts move between stages.

**Flow**:

```

Source (CodeCommit/GitHub/S3) → Build (CodeBuild) → Test → Deploy (CodeDeploy/ECS/S3)

````

---

## Step-by-Step Guide to Configure AWS CodePipeline

### Step 1: Create a Pipeline

1. Go to **AWS Management Console → CodePipeline → Pipelines → Create Pipeline**.
2. Provide:
   - **Pipeline Name**: e.g., `MyApp-Pipeline`
   - **Service Role**: Create new role or use existing IAM role
   - **Advanced Settings**: Enable artifact encryption if required
3. Click **Next**.

---

### Step 2: Configure Source Stage

1. Source Provider: **CodeCommit, GitHub, Bitbucket, S3**
2. Repository:
   - Select repository (e.g., `my-app-repo`)
   - Select branch (`main` or `dev`)
3. Change Detection Options:
   - Webhook (automatic trigger)
   - Polling (optional)
4. Click **Next**.

---

### Step 3: Configure Build Stage

1. Build Provider: **CodeBuild**
2. Create new CodeBuild project or select existing
   - Runtime: e.g., Node.js, Python, Java
   - Environment: Managed or custom image
   - Compute type: Small/Medium/Large
3. Buildspec: Use `buildspec.yml` in repository
4. Click **Next**.

---

### Step 4: Configure Deploy Stage

1. Deploy Provider: **CodeDeploy**, **Elastic Beanstalk**, **ECS**, or **S3**
2. Example with CodeDeploy:
   - Application name: `MyApp`
   - Deployment group: `MyApp-DeploymentGroup`
3. Click **Next**.

---

### Step 5: Review and Create Pipeline

- Review all stages and settings.
- Click **Create Pipeline**.
- CodePipeline automatically starts the first execution.

---

### Step 6: Monitor Pipeline Execution

1. Go to **Pipeline → Executions**
2. Monitor:
   - Stage status: In progress, succeeded, failed
   - Logs: CloudWatch (from CodeBuild or CodeDeploy)
3. Troubleshoot failed stages using logs and notifications.

---

## Practical Example: CI/CD for Node.js Application

### Scenario

- Repository: `nodejs-app-repo` in CodeCommit
- Goal: Automatically build, test, and deploy Node.js app to **Elastic Beanstalk** on code push.

### Step 1: CodeCommit Repository

- Repository Name: `nodejs-app-repo`
- Branch: `main`
- Contains `app.js`, `package.json`, and `buildspec.yml`.

### Step 2: buildspec.yml

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 18
    commands:
      - npm install
  build:
    commands:
      - npm test
  post_build:
    commands:
      - zip -r app.zip *

artifacts:
  files:
    - app.zip
````

### Step 3: Create CodePipeline

1. Source: CodeCommit (`nodejs-app-repo`, `main`)
2. Build: CodeBuild project (`NodejsApp-Build`)
3. Deploy: Elastic Beanstalk application (`NodejsApp-EB`)
4. On commit to `main`, pipeline triggers automatically:

   * CodeBuild installs dependencies, runs tests, and packages app
   * CodeDeploy/Elastic Beanstalk deploys package

### Step 4: Verify

* Push a commit to `main` branch:

```bash
git add .
git commit -m "Update app"
git push origin main
```

* CodePipeline executes stages sequentially.
* Elastic Beanstalk environment updates automatically.

---

## Best Practices

1. Use **separate stages** for source, build, test, and deploy.
2. Enable **manual approval** for production deployment.
3. Integrate with **CloudWatch** and **SNS** for notifications.
4. Use **buildspec.yml** for reproducible builds.
5. Use **IAM least privilege** for pipeline roles.
6. Store **artifacts in S3** for tracking and rollback.

---

## Summary

AWS CodePipeline provides a **fully automated CI/CD workflow**, enabling developers to deploy applications reliably and efficiently. It integrates seamlessly with CodeCommit, CodeBuild, CodeDeploy, and other AWS services to manage end-to-end software release processes.

**Practical Example**: Node.js app in CodeCommit → CodeBuild → Elastic Beanstalk deployment triggered automatically on code push demonstrates a typical CI/CD workflow.

---

**References**:

* [AWS CodePipeline Documentation](https://docs.aws.amazon.com/codepipeline/)
* [AWS DevOps Services Overview](https://aws.amazon.com/devops/)
