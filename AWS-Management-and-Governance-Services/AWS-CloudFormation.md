# 🏗️ **AWS CloudFormation — Infrastructure as Code (IaC)**

## 🧠 **What is AWS CloudFormation?**

**AWS CloudFormation** is a service that allows you to **define, provision, and manage AWS infrastructure as code** (IaC).
Instead of manually creating resources through the AWS Console, CLI, or SDK, you can use a **CloudFormation template** (written in **YAML** or **JSON**) to automate and standardize infrastructure deployment.

> 💡 In simple terms:
> CloudFormation = “Blueprint” for your AWS infrastructure.

---

## ⚙️ 1. **How It Works**

1. **You write a template**
   → Define AWS resources (like EC2, S3, VPC, IAM Roles, RDS, etc.) in YAML/JSON.

2. **Upload the template to CloudFormation**
   → You can do this via AWS Console, CLI, or S3 bucket.

3. **CloudFormation creates a “Stack”**
   → A **Stack** is a collection of AWS resources that CloudFormation provisions and manages together.

4. **It automatically handles dependencies**
   → For example, if an EC2 instance depends on a security group and subnet, CloudFormation creates them in the correct order.

5. **You can update or delete the Stack**
   → Updating the template changes infrastructure automatically.
   → Deleting the Stack removes all related resources.

---

## 🧩 2. **Key Components**

| **Component**       | **Description**                                                  |
| ------------------- | ---------------------------------------------------------------- |
| **Template**        | Blueprint of your AWS environment (in YAML/JSON).                |
| **Stack**           | A collection of AWS resources created from a template.           |
| **Change Set**      | Shows the impact of an update before applying it.                |
| **Drift Detection** | Detects manual changes made outside CloudFormation.              |
| **Stack Policy**    | Prevents accidental modification/deletion of critical resources. |

---

## 🪜 3. **Structure of a CloudFormation Template**

A typical template has these sections:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Create an EC2 instance and Security Group
Resources:
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH Access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
      SecurityGroups:
        - !Ref MySecurityGroup
```

---

## 🧩 4. **Basic Example – Creating an S3 Bucket**

Here’s a **simple YAML template** that creates an **S3 bucket**:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Create an S3 bucket using CloudFormation

Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-demo-cf-bucket-12345
      VersioningConfiguration:
        Status: Enabled
```

### 📝 Explanation:

| Section                      | Meaning                                                           |
| ---------------------------- | ----------------------------------------------------------------- |
| **AWSTemplateFormatVersion** | Version of CloudFormation template format                         |
| **Description**              | Short description of the stack                                    |
| **Resources**                | Main section — defines the AWS resources to create                |
| **Type**                     | AWS resource type (e.g., `AWS::S3::Bucket`, `AWS::EC2::Instance`) |
| **Properties**               | Configuration options for that resource                           |

✅ When you deploy this file, CloudFormation automatically:

* Creates an **S3 bucket**
* Enables **versioning**

---

## 💻 **How to Deploy (via AWS CLI)**

Save the above file as `s3bucket.yml`

Then run:

```bash
aws cloudformation create-stack \
  --stack-name MyS3Stack \
  --template-body file://s3bucket.yml
```

To check stack status:

```bash
aws cloudformation describe-stacks --stack-name MyS3Stack
```

To delete stack:

```bash
aws cloudformation delete-stack --stack-name MyS3Stack
```

---

## 🏗️ **Example 2 – EC2 Instance with Security Group**

A more realistic example creating an **EC2 instance** and **Security Group**:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Create EC2 instance and Security Group using CloudFormation

Resources:
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH and HTTP access
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c02fb55956c7d316  # Amazon Linux 2 (Example AMI)
      SecurityGroupIds:
        - !Ref MySecurityGroup
      KeyName: my-keypair
```

### 🧠 What this does:

* Creates a **Security Group** allowing SSH (22) and HTTP (80)
* Creates an **EC2 instance** using that SG
* Attaches an existing **Key Pair** for SSH login

---

## 🌐 **Example 3 – Full Stack (S3 + EC2 + IAM Role)**

Here’s a compact stack that creates:

1. An **S3 Bucket**
2. An **IAM Role** for EC2
3. An **EC2 instance** using that role

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: EC2 with IAM Role and S3 bucket

Resources:
  MyS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: cf-demo-bucket-12345

  EC2S3Role:
    Type: AWS::IAM::Role
    Properties:
      AssumeRolePolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: ec2.amazonaws.com
            Action: sts:AssumeRole
      Policies:
        - PolicyName: S3AccessPolicy
          PolicyDocument:
            Version: '2012-10-17'
            Statement:
              - Effect: Allow
                Action: ['s3:*']
                Resource: '*'

  MyInstanceProfile:
    Type: AWS::IAM::InstanceProfile
    Properties:
      Roles:
        - !Ref EC2S3Role

  MyEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-0c02fb55956c7d316
      IamInstanceProfile: !Ref MyInstanceProfile
      KeyName: my-keypair
```

### ⚙️ What happens:

* CloudFormation automatically creates an **IAM Role** for EC2 with **S3 full access**
* Then attaches that role to an EC2 instance
* The EC2 instance can now access S3 **securely (without access keys)**

---

## 🧭 5. **CloudFormation Drift Detection**

If a user manually changes a resource (e.g., modifies an EC2 security group in the console),
CloudFormation can **detect this drift** — showing which resources differ from the original template.

This is extremely useful for **governance and auditing**, ensuring infrastructure remains consistent with code-defined standards.

---

## 🛠️ 6. **Benefits of AWS CloudFormation**

| **Benefit**         | **Description**                                           |
| ------------------- | --------------------------------------------------------- |
| **Automation**      | Deploy complex environments with a single command.        |
| **Consistency**     | Same configuration every time — no manual errors.         |
| **Version Control** | Templates can be stored in Git for tracking changes.      |
| **Cost Control**    | Easily delete stacks to remove unused resources.          |
| **Compliance**      | Works with Config and CloudTrail to ensure governance.    |
| **Scalability**     | Use nested stacks and parameters for large-scale systems. |

---

## 🔒 7. **Real-World Example: DevOps Use Case**

You’re a **DevOps Engineer** at Infosys managing multiple environments (Dev, QA, Prod).
Instead of manually setting up EC2s, RDS, and Load Balancers each time:

* You create a **CloudFormation template** for the full stack.
* Deploy it with different parameter values for each environment.
* Track all infra changes via Git + CloudTrail.
* Detect unauthorized changes with **drift detection**.

✅ **Result:** Faster deployments, consistent infra, and easy rollback if something breaks.

---

## 🧾 8. **In Summary**

| **Feature**          | **Description**                                                       |
| -------------------- | --------------------------------------------------------------------- |
| **Service Type**     | Management & Governance                                               |
| **Purpose**          | Automate infrastructure creation and management as code               |
| **Template Format**  | YAML or JSON                                                          |
| **Core Concept**     | Stack = group of managed resources                                    |
| **Key Capabilities** | IaC, Drift Detection, Stack Policies, Change Sets                     |
| **Integrations**     | AWS Config, CloudTrail, Systems Manager                               |
| **Best For**         | Automated, consistent, version-controlled infrastructure provisioning |

---
