# 🛡️ Amazon IAM (Identity and Access Management) 

## 🧭 **Overview: What is AWS IAM?**

**AWS IAM (Identity and Access Management)** is a service that helps you securely control **access to AWS resources**.
It allows you to define **who can access (authentication)** and **what actions they can perform (authorization)** in your AWS account.

---

## 🧑‍💻 1️⃣ **IAM User**

### **Definition:**

An **IAM User** represents an **individual person or application** that interacts with AWS resources.

Each user:

* Has **unique credentials** (username, password, access keys).
* Can have **permissions** assigned **directly** or **through a group or policy**.

### **Example:**

Let’s say your team has 3 members — Dheeraj, Neha, and Raj.

* You create **IAM Users**:

  * `Dheeraj_User`
  * `Neha_User`
  * `Raj_User`

Each can log in to the AWS Console or use CLI with their credentials.

### **Use Case:**

Dheeraj is a DevOps Engineer who needs access to EC2 and S3 services.

➡️ Assign a policy that grants permissions for:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:*", "s3:*"],
      "Resource": "*"
    }
  ]
}
```

---

## 👥 2️⃣ **IAM Group**

### **Definition:**

A **Group** is a **collection of IAM Users**.
Groups help manage permissions for multiple users at once.

### **Example:**

You have a DevOps team with 10 members — instead of assigning policies individually, you can:

* Create a group: `DevOpsTeam`
* Attach a policy: `AmazonEC2FullAccess`
* Add users: `Dheeraj_User`, `Neha_User`, `Raj_User` → all automatically inherit EC2 access.

### **Use Case:**

When a new DevOps engineer joins, simply add them to `DevOpsTeam` → they get the same permissions.

---

## 📜 3️⃣ **IAM Policy**

### **Definition:**

A **policy** is a **JSON document** that defines **permissions** — specifying **allowed or denied actions** on AWS resources.

### **Structure:**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", 
      "Action": ["s3:PutObject", "s3:GetObject"], 
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

### **Key Elements:**

| Field         | Meaning                                        |
| ------------- | ---------------------------------------------- |
| **Effect**    | Allow or Deny                                  |
| **Action**    | AWS service actions (e.g., `s3:ListBucket`)    |
| **Resource**  | ARN (Amazon Resource Name) of target resource  |
| **Condition** | Optional rules (e.g., IP address restrictions) |

### **Example:**

A policy to allow uploading only to a specific S3 bucket:

```json
{
  "Effect": "Allow",
  "Action": ["s3:PutObject"],
  "Resource": "arn:aws:s3:::project-logs/*"
}
```

### **Use Case:**

Attach this policy to your `ApplicationUser` so it can upload logs to S3 but not delete them.

---

## 🎭 4️⃣ **IAM Role**

### **Definition:**

A **Role** is similar to a user, but it **does not have permanent credentials**.
Instead, it can be **assumed temporarily** by:

* AWS services (like EC2, Lambda)
* Other AWS accounts
* Federated users (SSO, identity providers)

Roles are used for **temporary, limited access** to perform specific actions.

---

### **Example:**

You have an **EC2 instance** that needs to read data from an **S3 bucket**.

Instead of embedding access keys in your app code:

* Create an IAM **Role** called `EC2S3AccessRole`
* Attach a policy:

```json
{
  "Effect": "Allow",
  "Action": ["s3:GetObject"],
  "Resource": "arn:aws:s3:::mybucket/*"
}
```

* Assign this role to your EC2 instance.

Now, EC2 can access S3 securely **without storing any credentials**.

---

### **Use Case (Cross-Service Access):**

A **Lambda function** wants to write logs to **CloudWatch**:

* Create a role `LambdaCloudWatchRole`
* Attach policy `CloudWatchFullAccess`
* Assign the role to your Lambda.

---

## 🧩 **Summary Table**

| Component  | Description                              | Example              | Best Use Case                               |
| ---------- | ---------------------------------------- | -------------------- | ------------------------------------------- |
| **User**   | Individual identity with credentials     | `Dheeraj_User`       | Human users needing AWS access              |
| **Group**  | Collection of users with shared policies | `DevOpsTeam`         | Assign same permissions to multiple users   |
| **Policy** | JSON document defining permissions       | `S3FullAccessPolicy` | Specify allowed/denied actions on resources |
| **Role**   | Temporary access without credentials     | `EC2S3AccessRole`    | Grant AWS services permissions securely     |

---

## 🌐 **Real-World Scenario**

**Scenario:**
Infosys DevOps team manages multiple AWS accounts.

* Dheeraj (DevOps Engineer) needs to automate deployment on EC2 and manage S3 buckets.
* QA team needs only read access to CloudWatch logs.
* EC2 instances need access to S3 for config files.

**Solution:**

1. Create `DevOpsGroup` → attach `AmazonEC2FullAccess` + `AmazonS3FullAccess`.
2. Create `QAGroup` → attach `CloudWatchReadOnlyAccess`.
3. Add users accordingly.
4. Create `EC2S3AccessRole` → attach `S3ReadOnlyAccess` and assign it to EC2.

✅ Secure
✅ Scalable
✅ Easy to manage

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
