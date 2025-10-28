# 🖥️ AWS EC2 (Elastic Compute Cloud)

## 🌐 What is EC2?
**Amazon EC2 (Elastic Compute Cloud)** is a core AWS service that provides **resizable virtual servers (instances)** in the cloud.  
You can launch, configure, and manage servers within minutes — just like renting a computer from AWS.

---

## ⚙️ How to Configure EC2
1. **Login** to AWS Management Console.  
2. Navigate to **EC2 Dashboard** → Click **Launch Instance**.  
3. Choose an **AMI (Amazon Machine Image)** (e.g., Amazon Linux, Ubuntu).  
4. Select an **Instance Type** (e.g., t2.micro).  
5. Configure **Network & Security**:
   - Choose VPC, Subnet.
   - Assign IAM Role (if needed).
6. Add **Storage** (EBS Volume or Instance Store).  
7. Configure **Security Group** (Firewall).  
8. Create or select an existing **Key Pair** for SSH access.  
9. Add **Tags** (like Name = “MyEC2Server”).  
10. Review and **Launch Instance**.

---
## 🧩 1. AMI (Amazon Machine Image)

An **Amazon Machine Image (AMI)** is a **pre-configured template** that contains all the information needed to **launch an EC2 instance** — including the **operating system, application server, and applications**.

In simple terms,
👉 **AMI = Operating System + Software + Configuration Settings**

It acts like a **“snapshot” or blueprint** of your instance.

---

###  **Key Components of an AMI**

1. **Root Volume Template** – The OS image (e.g., Linux, Windows).
2. **Launch Permissions** – Controls which AWS accounts can use the AMI.
3. **Block Device Mapping** – Specifies storage volumes attached at launch.

---

### 🧠 **Types of AMIs**

| **Type**             | **Description**                                                                                    | **Example**                                                                                       |
| -------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **AWS-Provided AMI** | Created and maintained by AWS. Includes standard OS images.                                        | Amazon Linux 2, Ubuntu, Windows Server 2022                                                       |
| **Marketplace AMI**  | Provided by third-party vendors for specific software needs.                                       | Bitnami WordPress AMI, Red Hat Enterprise Linux                                                   |
| **Custom AMI**       | Created by users from an existing configured instance. Useful for reusability and faster launches. | You install Java, Tomcat, and your app → create AMI → launch multiple servers with the same setup |
| **Community AMI**    | Shared publicly by other AWS users.                                                                | A free Ubuntu image shared by community users                                                     |

---

### 💡 **Example Scenario**

Let’s say you want to host a **Java web application** on EC2:

1. Launch an EC2 instance using the **Amazon Linux 2 AMI**.
2. Install **Java, Tomcat**, and deploy your application.
3. Once everything is configured, **create a custom AMI** from this instance.
4. Next time you need a similar server, just **launch it using your AMI** — no need to reinstall or reconfigure!

---

### ⚙️ **Example Command (AWS CLI)**

```bash
aws ec2 create-image \
  --instance-id i-0abcd1234efgh5678 \
  --name "MyAppServer-v1" \
  --description "Custom AMI with Java & Tomcat setup"
```

This command creates an AMI snapshot of the running instance named **MyAppServer-v1**.

---

## 💻 2. EC2 Instance Types
EC2 instance Types are broadly classified into 5 types based on the hardware configurations:

| **Type**                     | **Family**                  | **Description**                                                                                                             | **Typical Use Cases**                                                                                            | **Example Instances**                                  | **vCPU & Memory Range**    | **Storage Type**                       |
| ---------------------------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------------- | -------------------------------------- |
| 🟢 **General Purpose**       | `t`, `m`, `a`               | Balanced compute, memory, and networking resources for most workloads. Cost-effective and flexible.                         | Web servers, small/medium databases, development/test environments, microservices, backend servers               | `t3`, `t4g`, `m6i`, `m7g`, `a1`                        | 2–128 vCPUs, 0.5–512 GiB   | EBS only (Elastic Block Store)         |
| 🔵 **Compute Optimized**     | `c`                         | High-performance processors for compute-intensive applications. Offers best price-to-performance ratio for CPU-bound tasks. | High-performance web servers, scientific modeling, batch processing, media transcoding, gaming servers           | `c5`, `c6i`, `c7g`, `c7i`                              | 2–192 vCPUs, 4–384 GiB     | EBS only                               |
| 🟣 **Memory Optimized**      | `r`, `x`, `u`, `z`          | Designed for workloads that process large datasets in memory with high memory-to-CPU ratios. (fast performance)                               | In-memory caching (Redis, Memcached), SAP HANA, real-time big data analytics, high-performance databases         | `r6i`, `r7g`, `x2idn`, `x2iedn`, `u-6tb1.metal`, `z1d` | 2–448 vCPUs, 16–24,576 GiB | EBS or NVMe SSD                        |
| 🟠 **Accelerated Computing** | `p`, `g`, `inf`, `trn`, `f` | Equipped with GPUs, Inferentia, or FPGAs for specialized tasks requiring hardware acceleration.                             | Machine learning, Deep Learning, Seismic Analysis, 3D rendering, video encoding, scientific simulation, financial modeling | `p4d`, `p5`, `g5`, `inf2`, `trn1`, `f1`                | 8–192 vCPUs, 64–1,952 GiB  | EBS or NVMe SSD                        |
| 🔴 **Storage Optimized**     | `i`, `im`, `d`, `h`         | High IOPS and low latency for large data sets stored locally. Ideal for high-performance, data-intensive workloads.         | NoSQL/OLTP databases, big data analytics (Hadoop, Spark), log processing, data warehousing                       | `i3`, `i4i`, `i3en`, `im4gn`, `d2`, `h1`               | 2–128 vCPUs, 16–4,096 GiB  | NVMe SSD or HDD (local instance store) |

---
## 💰 3. EC2 Pricing Models

| **Pricing Model**                            | **Description**                                                                                                                                          | **Best For / Use Case**                                                                          | **Discount vs On-Demand**            | **Example**                                                                                                             |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| 🟢 **On-Demand Instances**                   | Pay only for compute capacity you use — by the second or hour. No upfront payment or long-term commitment.                                               | Short-term, unpredictable workloads that can’t be interrupted. Great for testing or development. | 0% (Base Price)                      | A startup launches a new web app and scales up or down daily. They pay per hour for `t3.medium` without reservation.    |
| 🔵 **Reserved Instances (RI)**               | Commit to a specific instance type in a specific region for 1 or 3 years in exchange for a lower hourly rate.                                            | Steady-state workloads with predictable usage.                                                   | Up to **75% cheaper** than On-Demand | A company runs a database server 24×7 and purchases a **3-year Standard Reserved Instance** for `m6i.large`.            |
| 🟠 **Spot Instances**                        | Use unused EC2 capacity at deep discounts. Prices fluctuate based on supply and demand.                                                                  | Flexible, fault-tolerant, interruptible workloads like big data, CI/CD, or testing.              | Up to **90% cheaper** than On-Demand | A data analytics team uses `c6i.4xlarge` Spot Instances for Hadoop batch jobs that can restart if interrupted.          |
| 🟣 **Savings Plans**                         | Commit to a consistent spend ($/hour) on EC2 or Fargate for 1 or 3 years, in exchange for discounts. More flexible than RIs (not tied to instance type). | Consistent workloads with flexible instance families or regions.                                 | Up to **72% cheaper** than On-Demand | A company commits to spend **$200/hour** on EC2 over 3 years, and AWS automatically applies discounts across instances. |
| 🔴 **Dedicated Hosts / Dedicated Instances** | Physical servers fully dedicated to your organization. Used for compliance, licensing, or isolation requirements.                                        | Workloads needing physical isolation or BYOL (Bring Your Own License).                           | No fixed discount — depends on usage | A finance company runs Oracle DB on a **Dedicated Host** to comply with licensing and regulatory requirements.          |
---


## 💾 4. EC2 Instance Storage

| **Storage Type**             | **Full Form**                 | **Description**                                                                                                                                            | **Persistence**  | **Performance**                               | **Best For / Use Case**                                                       | **Example Scenario**                                                                                                                                                |
| ---------------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | --------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🟢 **EBS Volume**            | **Elastic Block Store**       | A durable, block-level storage that attaches to your EC2 instance like a virtual hard drive. Data persists even after the instance stops or terminates.    | ✅ **Persistent** | High and consistent IOPS (SSD or HDD options) | Databases, web servers, boot volumes, or applications needing data durability | You launch an EC2 instance with an **8 GB gp3 EBS volume** to host a website. Even if you stop the instance, your website data stays safe.                          |
| 🔵 **Instance Store Volume** | **Ephemeral / Local Storage** | Physically attached disk storage on the same host as your EC2 instance. Offers very high I/O speed but data is lost when the instance stops or terminates. | ❌ **Temporary**  | Extremely fast (uses local SSD/NVMe)          | Temporary data, cache, or buffer storage that can be regenerated easily       | You run a **high-speed cache or big data job** on `i3.large` that uses **Instance Store NVMe SSD** for temporary processing. Once the instance stops, data is gone. |

---

### ⚙️ **Key Differences**

| **Feature**          | **EBS Volume**                                               | **Instance Store Volume**                   |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| **Data Persistence** | Data persists after instance stop/termination                | Data lost on stop/termination               |
| **Attach/Detach**    | Can attach/detach from any instance in the same AZ           | Tied to a specific instance                 |
| **Backup Support**   | Supports Snapshots (to S3)                                   | No backup or snapshot                       |
| **Durability**       | Highly durable (replicated across multiple AZ storage nodes) | Not durable (data loss on hardware failure) |
| **Performance**      | Consistent, can be provisioned for high IOPS                 | Very high raw performance (faster I/O)      |
| **Cost**             | Charged separately based on volume size and type             | Included in instance price                  |
| **Use Case**         | Databases, logs, application data                            | Temporary cache, buffer, scratch space      |

---

### 💡 **Example in Real Life**

| **Scenario**                                                  | **Storage Type Used** | **Why**                                                   |
| ------------------------------------------------------------- | --------------------- | --------------------------------------------------------- |
| Hosting a WordPress site with persistent data                 | **EBS Volume**        | Ensures the site files and database remain after restarts |
| Running Hadoop or Spark cluster for temporary data processing | **Instance Store**    | Fast local I/O and no need to retain intermediate data    |
---

## 🔒 5. Security Group

A **Security Group (SG)** in AWS acts as a **virtual firewall** that controls **inbound and outbound traffic** to your EC2 instance.

It defines **which traffic is allowed** to reach your instance and **which traffic your instance can send out**.

---

### ⚙️ **Key Characteristics**

| **Feature**          | **Description**                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------- |
| **Scope**            | Works at the **instance level**, not the subnet level (unlike Network ACLs).                         |
| **Stateful**         | Responses to allowed inbound traffic are automatically allowed outbound (and vice versa).            |
| **Default Behavior** | - All **inbound traffic is denied** by default.<br>- All **outbound traffic is allowed** by default. |
| **Rules Type**       | - **Inbound Rules** → Control incoming traffic.<br>- **Outbound Rules** → Control outgoing traffic.  |
| **Attachment**       | Each EC2 instance can have **one or more security groups** attached.                                 |

---

### 🧩 **Structure of a Security Group Rule**

| **Rule Type** | **Protocol** | **Port Range** | **Source/Destination** | **Purpose**                |
| ------------- | ------------ | -------------- | ---------------------- | -------------------------- |
| Inbound       | TCP          | 22             | 0.0.0.0/0              | Allow SSH from anywhere    |
| Inbound       | TCP          | 80             | 0.0.0.0/0              | Allow HTTP web traffic     |
| Inbound       | TCP          | 443            | 0.0.0.0/0              | Allow HTTPS web traffic    |
| Outbound      | All          | All            | 0.0.0.0/0              | Allow all outbound traffic |

---

### 🧠 **Example Scenario: Launching a Web Server**

You launched an EC2 instance running **Apache HTTP Server**.
To make it accessible via a browser and SSH:

#### ✅ **Step 1: Create a Security Group**

**Name:** `WebServer-SG`
**Description:** Allows web and SSH access

#### ✅ **Step 2: Add Inbound Rules**

| **Type** | **Protocol** | **Port Range** | **Source**                        | **Purpose**              |
| -------- | ------------ | -------------- | --------------------------------- | ------------------------ |
| SSH      | TCP          | 22             | Your IP (e.g., `203.0.113.25/32`) | Admin remote login       |
| HTTP     | TCP          | 80             | 0.0.0.0/0                         | Allow web traffic        |
| HTTPS    | TCP          | 443            | 0.0.0.0/0                         | Allow secure web traffic |

#### ✅ **Step 3: Add Outbound Rules**

| **Type**    | **Protocol** | **Port Range** | **Destination** | **Purpose**                                            |
| ----------- | ------------ | -------------- | --------------- | ------------------------------------------------------ |
| All traffic | All          | All            | 0.0.0.0/0       | Allow instance to reach internet for updates/downloads |

---

### 🌐 **How It Works**

* When someone opens `http://<Public-IP>` in a browser,
  the **HTTP (port 80)** rule in your SG allows that request.
* You can SSH into the instance using your **SSH rule (port 22)**.
* The **stateful nature** ensures response packets automatically return to the requester.

---

### 🔒 **Best Practices**

1. **Restrict SSH (22)** to your own IP only — never open to `0.0.0.0/0`.
2. Use **least privilege principle** — open only required ports.
3. Create **separate SGs** for layers (e.g., Web SG, DB SG).
4. Reference **another SG** as a source — e.g., allow traffic from Web SG to DB SG on port 3306.

---

### 🧩 **Example: Multi-Tier Setup**

| **Layer**       | **Security Group** | **Inbound Rules**                        | **Outbound Rules** |
| --------------- | ------------------ | ---------------------------------------- | ------------------ |
| Web Server      | `Web-SG`           | Allow HTTP (80), HTTPS (443), SSH (22)   | Allow all outbound |
| App Server      | `App-SG`           | Allow traffic from `Web-SG` on port 8080 | Allow to DB-SG     |
| Database Server | `DB-SG`            | Allow traffic from `App-SG` on port 3306 | Restrict outbound  |

This design ensures only **necessary communication paths** exist between tiers.

---

## 🔑 6. Key Pair
A **Key Pair** is used for **secure SSH or RDP login** to your instance.  
- `.pem` file (private key) → stored locally.  
- Public key → stored in AWS.  
Example:
```bash
ssh -i my-key.pem ec2-user@<public-ip>
```
---

## 🏷️ 7. Tags

Tags are **key-value pairs** used for identifying and organizing AWS resources.

Example:
* `Key = Name`, `Value = WebServer-Prod`
* Used for billing, automation, and management.

---

## 🧠 8. Practical Example

### Scenario: Deploying a Simple Web Server

**Goal:** Host a personal website using EC2.

### Steps:

1. **Launch Instance**

   * Choose AMI: `Amazon Linux 2`
   * Type: `t2.micro` (Free Tier)
   * Key Pair: `my-key.pem`
   * Security Group: Allow SSH (22), HTTP (80)
2. **Connect via SSH**

   ```bash
   ssh -i my-key.pem ec2-user@<public-ip>
   ```
3. **Install Apache**

   ```bash
   sudo yum update -y
   sudo yum install httpd -y
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```
4. **Deploy Website**

   ```bash
   echo "<h1>Hello from my EC2 Web Server!</h1>" | sudo tee /var/www/html/index.html
   ```
5. **Access**

   * Open browser → `http://<public-ip>`
   * You’ll see your hosted web page.

---

## ✅ 9. Summary

| Concept            | Description           |
| ------------------ | --------------------- |
| **EC2**            | Virtual server in AWS |
| **AMI**            | Template for instance |
| **EBS**            | Persistent storage    |
| **Instance Store** | Temporary storage     |
| **Security Group** | Virtual firewall      |
| **Key Pair**       | Secure login          |
| **Tags**           | Resource identifiers  |
| **Pricing**        | Multiple cost models  |

---

### 💡 Tip:

Use **AWS CloudWatch** to monitor CPU, memory, and disk usage of your EC2 instance.

---
