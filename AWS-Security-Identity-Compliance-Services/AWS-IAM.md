# 🛡️ Amazon IAM (Identity and Access Management) 

## 📘 What is AWS IAM?

**AWS Identity and Access Management (IAM)** is a **security service** that allows you to control **who can access your AWS resources (authentication)** and **what actions they can perform (authorization)**.  
It provides **fine-grained access control** across all AWS services.

In simple terms:
> IAM helps you securely manage access to AWS resources by creating users, assigning permissions, and defining policies.

IAM is a **global service** — it does not require region-specific configuration.

---

## 👤 IAM Principal

A **Principal** is an **entity that can perform actions on AWS resources**.  
Principals can be:
- **IAM Users**
- **IAM Roles**
- **AWS Services** (like EC2, Lambda)
- **Federated Users** (from external identity providers like Google or Active Directory)

Example:  
If an EC2 instance assumes a role to access S3, then **EC2 is the principal**.

---

## 👨‍💻 IAM User vs Root User

### 🧑‍💼 IAM User
- Created and managed within IAM by the root account.
- Each user has **unique credentials** (username, password, access keys).
- IAM Users are assigned **permissions** via **policies**.
- Typically represents a **person or application** needing AWS access.

### 👑 Root User
- Created when you first open your AWS account.
- Has **unrestricted access** to **all** AWS resources and billing.
- **Best practice:** Use the root user only for **initial setup and billing tasks**.

| Feature | Root User | IAM User |
|----------|------------|----------|
| Permissions | Full access | Restricted (as defined) |
| Usage | Account setup, billing | Daily operations |
| Security Risk | High | Low (if managed well) |

---

## 👥 IAM Group

An **IAM Group** is a **collection of IAM Users**.  
Groups make it easier to manage permissions for multiple users at once.

Example:
- Create a group called **Developers**
- Attach a **policy** that allows EC2 and S3 access
- Add users **John**, **Alice**, and **Raj** to the group  
→ All members get EC2 and S3 access.

Groups **cannot** contain other groups.

---

## 🎭 IAM Role

An **IAM Role** is similar to a user but **does not have credentials** (like passwords or access keys).  
Roles are **assumed temporarily** by trusted entities (users, applications, or AWS services).

Use Cases:
- EC2 instance needing S3 access.
- Lambda function accessing DynamoDB.
- Cross-account access (account A granting permissions to account B).

Example:
> You can create a role that grants **S3 read access** and attach it to an **EC2 instance**.  
The instance can now read from S3 without storing any access keys locally.

---

## 📜 IAM Policies

**Policies** define **permissions** in JSON format.  
They specify:
- **Who** can access (Principal)
- **What actions** they can perform (Action)
- **Which resources** they can act upon (Resource)
- **Under what conditions** (Condition)

### Example Policy (Allow EC2 read-only access):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    }
  ]
}
````

**Types of Policies:**

1. **AWS Managed Policies** – Created and maintained by AWS.
2. **Customer Managed Policies** – Created by you for specific needs.
3. **Inline Policies** – Directly attached to a single user, group, or role.

---

## 🔐 IAM Security Best Practices

1. **Never use the root user** for daily tasks.
2. **Enable MFA (Multi-Factor Authentication)** for all users.
3. **Use groups** to manage permissions instead of attaching policies to individual users.
4. **Grant least privilege access** – only what’s necessary.
5. **Rotate access keys** regularly.
6. **Use IAM roles** for applications instead of embedding credentials.
7. **Monitor IAM activity** using **AWS CloudTrail**.
8. **Use policy conditions** for time-based or IP-based access control.
9. **Review IAM policies** periodically with **IAM Access Analyzer**.
10. **Enforce password policies** for strong authentication.

---

## 💰 Pricing

AWS IAM is **free of charge**.
You can create and manage users, groups, roles, and policies without cost.

However:

* You pay for **AWS resources** accessed via IAM (e.g., S3, EC2).
* **IAM Access Analyzer** incurs charges only for **advanced features**.

---

## 🧠 Practical Example: EC2 Accessing S3 via IAM Role

### Scenario:

You want your **EC2 instance** to **read data from an S3 bucket** without manually storing access keys.

### Steps:

#### Step 1: Create an IAM Role

* Go to **IAM → Roles → Create role**
* Choose **Trusted Entity:** AWS Service → EC2
* Attach **AmazonS3ReadOnlyAccess** policy
* Name it: `EC2S3ReadRole`

#### Step 2: Attach Role to EC2 Instance

* Launch or select an existing EC2 instance.
* Under **Actions → Security → Modify IAM Role**, attach `EC2S3ReadRole`.

#### Step 3: Verify Access

* SSH into your EC2 instance
* Run:

  ```bash
  aws s3 ls
  ```
* The command should list all accessible S3 buckets (no credentials needed).

---

## ✅ Summary

| Component     | Description                                        |
| ------------- | -------------------------------------------------- |
| **IAM**       | Securely controls access to AWS resources          |
| **Principal** | Entity that performs actions (user, role, service) |
| **IAM User**  | Individual identity with credentials               |
| **Root User** | Account owner with full access                     |
| **IAM Group** | Collection of IAM users                            |
| **IAM Role**  | Temporary credentials for AWS services or users    |
| **Policy**    | JSON document defining permissions                 |
| **Security**  | MFA, least privilege, monitoring, roles            |
| **Pricing**   | Free (pay only for used resources)                 |

---

### 🔍 Real-world Example Summary:

> In a production setup, IAM ensures **secure, temporary, and auditable access** for all AWS entities.
> Using IAM roles for EC2, CloudWatch, Lambda, or CodePipeline allows automation without compromising security.

---

Would you like me to **save this as a downloadable `.md` file** for you (so you can upload it to GitHub or your DevOps notes folder)?
```
