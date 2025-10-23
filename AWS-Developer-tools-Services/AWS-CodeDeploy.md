# AWS CodeDeploy

## What is AWS CodeDeploy?

**AWS CodeDeploy** is a fully managed **deployment service** that automates application deployments to a variety of compute services such as **Amazon EC2, AWS Lambda, and on-premises servers**.  

CodeDeploy enables you to rapidly release new features, helps avoid downtime during deployment, and handles the complexity of updating your applications.

---

## Key Features of AWS CodeDeploy

1. **Automated Deployments**: Automatically deploys applications to compute resources.
2. **Multiple Deployment Targets**:
   - **EC2 Instances**
   - **On-premises servers**
   - **AWS Lambda**
   - **Amazon ECS (with CodeDeploy ECS integration)**
3. **Deployment Types**:
   - **In-place Deployment**: Updates application on existing instances.
   - **Blue/Green Deployment**: Shifts traffic to a new set of instances while minimizing downtime.
4. **Rollbacks**: Automatic rollback if deployment fails.
5. **Fine-Grained Deployment Control**:
   - Deployment configurations (e.g., 50% at a time)
   - Hooks and lifecycle events
6. **Integration with CI/CD**:
   - AWS CodePipeline
   - CodeBuild
   - GitHub, Bitbucket
7. **Monitoring and Logging**: Integration with CloudWatch, SNS notifications, and deployment logs.

---

## AWS CodeDeploy Architecture

1. **Application**: Logical unit representing your deployable code.
2. **Deployment Group**:
   - Defines **target instances**
   - Sets **deployment configuration** (e.g., all-at-once, rolling, or canary)
   - Associates **IAM roles** for deployment
3. **Revision**:
   - Version of application code stored in S3, CodeCommit, or GitHub
4. **Deployment**:
   - Process of installing a specific revision on instances
   - Supports hooks at various stages (BeforeInstall, AfterInstall, ApplicationStart, ValidateService)
5. **Compute Resources**:
   - EC2, On-premises, Lambda, ECS

**Flow**:

```

Source (S3/CodeCommit/GitHub) → CodeDeploy Application → Deployment Group → Target Instances → Deployment

````

---

## Step-by-Step Guide to Configure AWS CodeDeploy

### Step 1: Create IAM Role for CodeDeploy

1. Go to **IAM Console → Roles → Create Role**
2. Select **AWS Service → CodeDeploy**
3. Attach Policy: `AWSCodeDeployRole`
4. Name Role: `CodeDeployServiceRole`
5. This role allows CodeDeploy to access EC2 instances and deployment artifacts.

---

### Step 2: Install CodeDeploy Agent on EC2

- EC2 instances must have **CodeDeploy agent** installed to receive deployments.

**Amazon Linux 2 example**:

```bash
sudo yum update -y
sudo yum install ruby -y
cd /home/ec2-user
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent start
sudo service codedeploy-agent status
````

---

### Step 3: Create a CodeDeploy Application

1. Go to **AWS CodeDeploy → Applications → Create Application**
2. Name: `MyApp`
3. Compute Platform: `EC2/On-premises` or `Lambda`
4. Click **Create Application**

---

### Step 4: Create a Deployment Group

1. Go to **MyApp → Deployment Groups → Create Deployment Group**
2. Name: `MyApp-DeploymentGroup`
3. Deployment Type:

   * **In-place** (updates existing instances)
   * **Blue/Green** (new instances for deployment)
4. Environment Configuration:

   * Choose **EC2 Instances**
   * Select **tags** or **Auto Scaling Group**
5. Service Role: `CodeDeployServiceRole`
6. Deployment Configuration:

   * All-at-once, Half-at-a-time, Custom
7. Click **Create Deployment Group**

---

### Step 5: Prepare Application Revision

1. Structure of revision package:

```
my-app/
├── appspec.yml
├── scripts/
│   ├── install_dependencies.sh
│   └── start_server.sh
├── index.html
```

2. `appspec.yml` example:

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
      timeout: 300
      runas: root
```

3. Package revision as **ZIP** or **tar.gz**.
4. Upload to **S3** or commit to **CodeCommit**.

---

### Step 6: Create Deployment

1. Go to **CodeDeploy → Applications → MyApp → Create Deployment**
2. Deployment Type: In-place or Blue/Green
3. Select Revision:

   * S3: s3://bucket/my-app.zip
   * CodeCommit: Repository and branch
4. Select Deployment Group: `MyApp-DeploymentGroup`
5. Click **Deploy**
6. Monitor Deployment Progress:

   * Successful, Failed, or In-progress
   * Check **Deployment Logs** on EC2 (`/var/log/aws/codedeploy-agent/codedeploy-agent.log`)

---

## Practical Example: Deploy Static Website to EC2

### Scenario

* Static website files in CodeCommit repository `my-website`
* Goal: Deploy to EC2 instances using CodeDeploy

### Step 1: CodeCommit Repository

```
my-website/
├── appspec.yml
├── index.html
├── scripts/
│   ├── install_dependencies.sh
│   └── start_server.sh
```

`appspec.yml`:

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /var/www/html
hooks:
  BeforeInstall:
    - location: scripts/install_dependencies.sh
      runas: root
  ApplicationStart:
    - location: scripts/start_server.sh
      runas: root
```

`scripts/install_dependencies.sh`:

```bash
#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
```

`scripts/start_server.sh`:

```bash
#!/bin/bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

### Step 2: Create CodeDeploy Application

* Application: `MyWebsiteApp`
* Deployment Group: `MyWebsite-DG`
* Target EC2 Instances: Tag `App=MyWebsite`

### Step 3: Deploy

* Deployment Type: In-place
* Source: CodeCommit `my-website`, branch `main`
* CodeDeploy pushes revision to EC2 and executes hooks
* Website becomes live on EC2 instances

### Step 4: Verify

* Access EC2 Public IP in browser:

```text
http://<EC2-PUBLIC-IP>/
```

* Static website should load successfully.

---

## Best Practices

1. Use **Blue/Green deployment** for production to reduce downtime.
2. Keep **appspec.yml** organized with hooks for automation.
3. Monitor deployments with **CloudWatch** and **SNS** notifications.
4. Ensure **IAM roles** have least privilege access.
5. Use **tags or Auto Scaling groups** for scalable deployments.
6. Test deployments in **staging** before production.

---

## Summary

AWS CodeDeploy automates deployment processes, reduces downtime, and ensures reliable software delivery across EC2, Lambda, ECS, and on-premises servers.

**Practical Example**: Deploying a static website to EC2 using CodeDeploy automates dependency installation, starts the web server, and ensures consistent deployments.

---

**References**:

* [AWS CodeDeploy Documentation](https://docs.aws.amazon.com/codedeploy/)
* [AWS DevOps Services Overview](https://aws.amazon.com/devops/)
