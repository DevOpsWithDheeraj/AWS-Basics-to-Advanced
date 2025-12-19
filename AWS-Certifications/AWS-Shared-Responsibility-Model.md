
# **🌩️ AWS Shared Responsibility Model**

The **AWS Shared Responsibility Model** defines **who is responsible for what** when you use AWS services.

It splits responsibility into two parts:

---

## **1️⃣ AWS Responsibility – “Security *OF* the Cloud”**

AWS manages and protects everything that runs **AWS infrastructure**.

### AWS is responsible for:

* 🏢 **Physical security** of data centers
* 🔐 **Hardware, networking, storage devices**
* ⚙️ **Hypervisors (virtualization layer)**
* 🛡️ **Global infrastructure**

  * Regions
  * Availability Zones
  * Edge locations
* ⚙️ **Managed services infrastructure**

  * S3 durability
  * DynamoDB availability
  * EBS replication
  * CloudFront global network

### **Example**

If an AWS data center gets flooded, or a storage disk fails → **AWS must handle it**, not you.

---

## **2️⃣ Customer Responsibility – “Security *IN* the Cloud”**

You (the user) are responsible for securing **everything you put inside AWS**.

### Customer is responsible for:

* 🔑 **IAM (users, roles, policies)**
* 🔒 **Data protection**

  * Your data encryption
  * Your backup strategy
* 🛡️ **Network security**

  * Security Groups
  * NACLs
* 🏷️ **Patching EC2 OS & applications**
* 🚀 **Application code security**

  * Vulnerability scanning
  * Secrets management (SSM, Secrets Manager)

### **Example**

If your EC2 instance is hacked because you used a weak password or open port 22 to the world → **your mistake**, not AWS’s.

---

## **3️⃣ Shared Responsibility (Depends on Service Type)**

Some AWS services shift responsibilities based on usage:

---

## **A. Infrastructure Services (EC2, EBS, VPC)**

Customer manages:

* OS patching
* Firewall rules
* Application config

AWS manages:

* Hardware
* Networking
* Data center

**Example**
You run a Java app on EC2 → You patch Java & Linux.
AWS manages only the EC2 hardware and power.

---

## **B. Container Services (ECS, EKS, Fargate)**

Shared:

| Component                           | AWS | Customer |
| ----------------------------------- | --- | -------- |
| EC2 hardware                        | ✔️  | ❌        |
| Kubernetes Control Plane (EKS)      | ✔️  | ❌        |
| Worker nodes (if self-managed)      | ❌   | ✔️       |
| Container images & application code | ❌   | ✔️       |

**Example: EKS**
AWS manages the control plane.
You manage worker node patching & pod security.

---

## **C. Fully Managed Services (S3, DynamoDB, Lambda)**

AWS manages:

* Infrastructure
* OS
* Patching
* Scaling

Customer manages:

* Data
* Access permissions
* Application logic

**Example: Lambda**
AWS handles servers & runtime.
You write and secure your code.

---

# **🔥 Real DevOps Example**

### **If your S3 bucket becomes public and data leaks → Who is responsible?**

👉 **Customer fault** (misconfigured bucket policy)

### **If S3 service goes down in a region → Who is responsible?**

👉 **AWS fault** (service availability)

### **If EC2 isn't patched and gets infected**

👉 **Customer responsibility**

---

# **🧠 Summary Table**

| Responsibility                  | AWS | Customer |
| ------------------------------- | --- | -------- |
| Data Centers                    | ✔️  | ❌        |
| Hardware                        | ✔️  | ❌        |
| Network Infrastructure          | ✔️  | ❌        |
| Managed Services Infrastructure | ✔️  | ❌        |
| Identity & Access, Encryption   | ❌   | ✔️       |
| OS Patching on EC2              | ❌   | ✔️       |
| Application Code                | ❌   | ✔️       |
| Data Security                   | ❌   | ✔️       |

---
