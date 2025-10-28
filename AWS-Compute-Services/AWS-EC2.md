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

## 💻 1. Instance Types
EC2 instance Types are broadly classified into 5 types based on the hardware configurations:

| **Type**                     | **Instance Family**                                           | **Use Cases**                                                                                                                                       | **Examples**                                                                                                                                                     |
| ---------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🟢 **General Purpose**       | **T, M, A** families (e.g., t3, t4g, m5, m6g, a1)             | Balanced compute, memory, and networking resources. Best for web servers, small databases, dev/test environments, and microservices.      | **t3.micro** – low-cost dev/test <br> **m6g.large** – general app hosting <br> **a1.medium** – ARM-based workloads                                               |
| 🔵 **Compute Optimized**     | **C** family (e.g., c5, c6g, c7g)                             | High-performance processors for compute-intensive tasks like gaming servers, scientific modeling, batch processing, and machine learning inference. | **c5.xlarge** – high compute tasks <br> **c7g.large** – ARM Graviton3 workloads                                                                                  |
| 🟣 **Memory Optimized**      | **R, X, Z, u** families (e.g., r5, r6g, x1e, z1d)             | For memory-heavy applications like in-memory databases, caching, real-time big data analytics, and high-performance computing (HPC).              | **r6g.xlarge** – in-memory cache (Redis) <br> **x1e.32xlarge** – SAP HANA <br> **z1d.large** – electronic design automation (EDA)                                |
| 🟠 **Accelerated Computing** | **P, G, F, Trn, Inf** families (e.g., p4, g5, f1, trn1, inf1) | Use GPUs, FPGAs, or custom chips for ML training/inference, video rendering, deep learning, and scientific simulations.                             | **p4d.24xlarge** – deep learning training <br> **g5.xlarge** – graphics rendering <br> **f1.2xlarge** – FPGA-based workloads <br> **inf2.xlarge** – ML inference |
| 🟤 **Storage Optimized**     | **I, D, H, Im, Is** families (e.g., i3, i4i, d2, h1)          | Designed for high, sequential read/write access to large data sets—ideal for databases, big data analytics, and data warehousing.       | **i3.large** – NoSQL databases <br> **i4i.4xlarge** – transactional DBs <br> **d2.8xlarge** – data warehouse workloads                                           |

---

| **Type**                  | **Family**                  | **Description / Use Cases**                                                                                                                     | **Examples**                                                                                                                                                            |
| ------------------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **General Purpose**       | `t`, `m`, `a`               | Balanced compute, memory, and networking resources. Best for applications that use these resources in equal proportions.                        | - `t3`, `t4g` → Low-cost, burstable workloads<br>- `m6i`, `m7g` → Web/app servers, small & medium databases, development environments                                   |
| **Compute Optimized**     | `c`                         | Designed for compute-intensive tasks that require high CPU performance. Ideal for workloads that benefit from fast processors.                  | - `c6i`, `c7g` → High-performance web servers, scientific modeling, gaming servers, batch processing, media transcoding                                                 |
| **Memory Optimized**      | `r`, `x`, `u`, `z`          | Deliver high memory-to-CPU ratios for memory-intensive workloads. Best for applications that process large datasets in memory.                  | - `r6i`, `r7g` → In-memory caches (Redis, Memcached), big data analytics<br>- `x2idn`, `z1d` → SAP HANA, real-time analytics, large relational databases                |
| **Accelerated Computing** | `p`, `inf`, `trn`, `g`, `f` | Use hardware accelerators (GPUs, FPGAs, or Inferentia chips) for floating-point calculations, graphics, or machine learning inference/training. | - `p4d`, `p5` → Deep learning training<br>- `g5` → Graphics rendering, video encoding<br>- `inf2`, `trn1` → ML inference & training<br>- `f1` → FPGA-based acceleration |
| **Storage Optimized**     | `i`, `im`, `d`, `h`         | Designed for high, sequential read/write access to large data sets on local storage. Ideal for database and big data workloads.                 | - `i4i`, `i3en` → NoSQL databases, OLTP systems<br>- `d2`, `h1` → Data warehousing, Hadoop distributed storage, log processing                                          |

---
| **Type**                     | **Family**                  | **Description**                                                                                                             | **Typical Use Cases**                                                                                            | **Example Instances**                                  | **vCPU & Memory Range**    | **Storage Type**                       |
| ---------------------------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------------- | -------------------------------------- |
| 🟢 **General Purpose**       | `t`, `m`, `a`               | Balanced compute, memory, and networking resources for most workloads. Cost-effective and flexible.                         | Web servers, small/medium databases, development/test environments, microservices, backend servers               | `t3`, `t4g`, `m6i`, `m7g`, `a1`                        | 2–128 vCPUs, 0.5–512 GiB   | EBS only (Elastic Block Store)         |
| 🔵 **Compute Optimized**     | `c`                         | High-performance processors for compute-intensive applications. Offers best price-to-performance ratio for CPU-bound tasks. | High-performance web servers, scientific modeling, batch processing, media transcoding, gaming servers           | `c5`, `c6i`, `c7g`, `c7i`                              | 2–192 vCPUs, 4–384 GiB     | EBS only                               |
| 🟣 **Memory Optimized**      | `r`, `x`, `u`, `z`          | Designed for workloads that process large datasets in memory with high memory-to-CPU ratios.                                | In-memory caching (Redis, Memcached), SAP HANA, real-time big data analytics, high-performance databases         | `r6i`, `r7g`, `x2idn`, `x2iedn`, `u-6tb1.metal`, `z1d` | 2–448 vCPUs, 16–24,576 GiB | EBS or NVMe SSD                        |
| 🟠 **Accelerated Computing** | `p`, `g`, `inf`, `trn`, `f` | Equipped with GPUs, Inferentia, or FPGAs for specialized tasks requiring hardware acceleration.                             | Machine learning (training & inference), 3D rendering, video encoding, scientific simulation, financial modeling | `p4d`, `p5`, `g5`, `inf2`, `trn1`, `f1`                | 8–192 vCPUs, 64–1,952 GiB  | EBS or NVMe SSD                        |
| 🔴 **Storage Optimized**     | `i`, `im`, `d`, `h`         | High IOPS and low latency for large data sets stored locally. Ideal for high-performance, data-intensive workloads.         | NoSQL/OLTP databases, big data analytics (Hadoop, Spark), log processing, data warehousing                       | `i3`, `i4i`, `i3en`, `im4gn`, `d2`, `h1`               | 2–128 vCPUs, 16–4,096 GiB  | NVMe SSD or HDD (local instance store) |

---

## 💾 2. EBS Volume
**EBS (Elastic Block Store)** provides **persistent storage** for EC2 instances.  
- It behaves like a hard drive that remains even after instance termination (if not deleted).  
- You can take **snapshots** for backup or attach to another instance.  

Example: `/dev/xvda` → Root EBS Volume.

---

## ⚡ 3. Instance Store
- Temporary storage physically attached to the host.  
- **Faster**, but data is **lost** if instance stops or terminates.  
- Best for **caching, buffer, or temporary data**.

---

## 🧩 4. AMI (Amazon Machine Image)

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

## 🔒 5. Security Group
A **Security Group** acts as a **virtual firewall** that controls inbound and outbound traffic.  
Example Rules:
- Inbound: Allow TCP 22 (SSH) from your IP  
- Outbound: Allow all traffic  

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

## 💰 8. Pricing

EC2 pricing models:

| Model             | Description             | Example                        |
| ----------------- | ----------------------- | ------------------------------ |
| **On-Demand**     | Pay per hour/second     | Testing or short-term apps     |
| **Reserved**      | 1 or 3-year commitment  | Long-term predictable workload |
| **Spot**          | Bid for unused capacity | Batch jobs, flexible tasks     |
| **Savings Plans** | Flexible discount model | Commitment to consistent usage |

---



## 🧠 9. Practical Example

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

## ✅ 10. Summary

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
