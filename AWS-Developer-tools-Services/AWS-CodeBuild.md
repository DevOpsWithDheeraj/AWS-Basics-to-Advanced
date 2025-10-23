# AWS CodeBuild

## What is AWS CodeBuild?

**AWS CodeBuild** is a fully managed **continuous integration (CI) service** that compiles source code, runs tests, and produces software packages ready for deployment. It scales automatically and eliminates the need to provision or manage build servers.

CodeBuild integrates with AWS DevOps tools like **CodeCommit**, **CodePipeline**, **CodeDeploy**, and external tools such as GitHub, Bitbucket, and GitLab.

---

## Key Features of AWS CodeBuild

1. **Fully Managed Build Service**: No server management required.
2. **Continuous Scaling**: Automatically scales to handle multiple builds concurrently.
3. **Pay-as-You-Go**: Pay only for the compute time consumed.
4. **Custom Build Environments**: Use preconfigured environments or create custom Docker images.
5. **Integration with AWS Services**:
   - Source: CodeCommit, S3, GitHub, Bitbucket
   - Deploy: CodeDeploy, S3, ECS, EKS
   - CI/CD: CodePipeline
6. **Build Specifications (buildspec.yml)**: Defines build commands, environment variables, and artifacts.
7. **Encryption and Security**: Integrates with IAM for access control and KMS for artifact encryption.
8. **Logging & Monitoring**: Real-time logs via CloudWatch, S3, and CodeBuild console.
9. **Environment Variables**: Supports parameterized builds.

---

## AWS CodeBuild Architecture

1. **Source**: Where the code resides (CodeCommit, GitHub, S3, etc.).
2. **Build Environment**: EC2 instances running preconfigured or custom Docker images.
3. **Buildspec File**: YAML file defining phases like install, pre_build, build, post_build, and artifacts.
4. **Artifacts**: Output of the build process (e.g., compiled binaries, Docker images, packages).
5. **Logs**: Monitors build progress and stores logs in CloudWatch or S3.
6. **Build Project**: Configuration for CodeBuild specifying source, environment, compute resources, and artifacts.

**Flow**:

- Source → CodeBuild → Build Phases → Generate Artifacts → Push to S3, ECR, or Deploy

---

## Step-by-Step Guide to Configure AWS CodeBuild

### Step 1: Create a Build Project

1. Go to **AWS Management Console → CodeBuild → Build Projects → Create Build Project**.
2. Provide:
   - **Project Name**: e.g., `MyApp-Build`
   - **Description**: Optional
3. **Source Configuration**:
   - Source Provider: CodeCommit, GitHub, S3, Bitbucket
   - Repository: Select repository (e.g., `my-app-repo`)
   - Branch: `main` or `dev`
4. **Environment**:
   - Environment Image: Managed image (Amazon Linux 2 / Ubuntu / Windows) or Custom image
   - Compute Type: `BUILD_GENERAL1_SMALL/Medium/Large`
   - Privileged Mode: Enable for Docker builds
5. **Service Role**:
   - Use existing IAM role or create new role with `AWSCodeBuildAdminAccess`
6. **Buildspec**:
   - Use **buildspec.yml in source** or define inline commands
7. **Artifacts**:
   - Type: S3 bucket or no artifacts
   - Path: `build/`
8. **Logs**:
   - Enable CloudWatch logs for monitoring

---

### Step 2: Create buildspec.yml

`buildspec.yml` defines the build process and can be placed in the repository root.

Example for Python project:

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      python: 3.10
    commands:
      - pip install -r requirements.txt
  pre_build:
    commands:
      - echo "Running pre-build tasks"
  build:
    commands:
      - echo "Starting build process"
      - python -m unittest discover tests
  post_build:
    commands:
      - echo "Build completed successfully"

artifacts:
  files:
    - '**/*'
  base-directory: build
````

---

### Step 3: Trigger Builds

* **Manual Trigger**: Click **Start Build** in CodeBuild console.
* **Automatic Trigger**:

  * Integrate with **CodePipeline**
  * Use **webhooks** for GitHub/Bitbucket to trigger builds on push or pull request.

---

### Step 4: Monitor Builds

1. Check **Build History** in CodeBuild console.
2. View **Build Logs**:

   * Real-time via CloudWatch
   * Stored in S3 if configured
3. View **Build Artifacts** in S3 or ECR.

---

### Step 5: Integrate with CI/CD Pipeline (Optional)

1. Go to **CodePipeline → Create Pipeline**.
2. Add **Source Stage**: CodeCommit repo
3. Add **Build Stage**: CodeBuild project
4. Add **Deploy Stage**: CodeDeploy, ECS, or S3
5. On commit to main branch, CodePipeline triggers CodeBuild → Build → Deploy automatically.

---

## Practical Example: Build and Test Node.js App

### Scenario

* Repository: `nodejs-app-repo` (CodeCommit)
* Goal: Install dependencies, run tests, and save build artifacts in S3

### Step 1: Create CodeBuild Project

* Project Name: `NodejsApp-Build`
* Source: CodeCommit (`nodejs-app-repo`, branch `main`)
* Environment: Managed Ubuntu image, Node.js 18 runtime
* Artifacts: S3 bucket `my-app-build-artifacts`
* Logs: CloudWatch

### Step 2: Add buildspec.yml in Repository

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
      - mkdir build
      - cp -r * build/

artifacts:
  files:
    - '**/*'
  base-directory: build
```

### Step 3: Trigger Build

```bash
git add buildspec.yml
git commit -m "Add buildspec for CodeBuild"
git push origin main
```

* CodeBuild automatically installs dependencies, runs tests, and stores build artifacts in S3.

### Step 4: Verify

* Check **CloudWatch Logs** for build output.
* Artifacts are available in configured **S3 bucket**.

---

## Best Practices

1. Use **buildspec.yml** for reproducible builds.
2. Enable **CloudWatch Logs** for monitoring.
3. Use **IAM least privilege** for build roles.
4. Use **caching** to speed up builds for dependencies.
5. Enable **automatic triggers** via CodePipeline or webhooks.
6. Separate build environments for **dev, test, prod**.

---

## Summary

AWS CodeBuild is a **fully managed CI service** that automates building, testing, and packaging applications. It integrates with CodeCommit, CodePipeline, and CodeDeploy for complete DevOps workflows.

**Practical Example**: Building a Node.js application from CodeCommit, running tests, and storing artifacts in S3 using a `buildspec.yml` file demonstrates a typical CI process.

---

**References**:

* [AWS CodeBuild Documentation](https://docs.aws.amazon.com/codebuild/)
* [AWS DevOps Tools Overview](https://aws.amazon.com/devops/)
