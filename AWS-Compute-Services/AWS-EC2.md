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

## 💻 Instance Types
EC2 instances come in families optimized for different workloads:

| Type | Family | Use Case |
|------|---------|----------|
| **t2/t3** | General Purpose | Web servers, small apps |
| **m5/m6** | Balanced | Application servers |
| **c5/c6** | Compute Optimized | High-performance compute |
| **r5/r6** | Memory Optimized | Databases, analytics |
| **p3/g4** | GPU Optimized | AI/ML, graphics rendering |
| **i3/d2/h1** | Storage Optimized | Big data, high I/O apps |

---

## 💾 EBS Volume
**EBS (Elastic Block Store)** provides **persistent storage** for EC2 instances.  
- It behaves like a hard drive that remains even after instance termination (if not deleted).  
- You can take **snapshots** for backup or attach to another instance.  

Example: `/dev/xvda` → Root EBS Volume.

---

## ⚡ Instance Store
- Temporary storage physically attached to the host.  
- **Faster**, but data is **lost** if instance stops or terminates.  
- Best for **caching, buffer, or temporary data**.

---

## 🧩 AMI (Amazon Machine Image)
An **AMI** is a pre-configured template used to launch EC2 instances.  
It contains:
- OS (e.g., Linux, Windows)
- Application server
- Configurations

You can also **create custom AMIs** from existing instances.

---

## 🔒 Security Group
A **Security Group** acts as a **virtual firewall** that controls inbound and outbound traffic.  
Example Rules:
- Inbound: Allow TCP 22 (SSH) from your IP  
- Outbound: Allow all traffic  

---

## 🔑 Key Pair
A **Key Pair** is used for **secure SSH or RDP login** to your instance.  
- `.pem` file (private key) → stored locally.  
- Public key → stored in AWS.  
Example:
```bash
ssh -i my-key.pem ec2-user@<public-ip>
```
---

## 🏷️ Tags

Tags are **key-value pairs** used for identifying and organizing AWS resources.

Example:
* `Key = Name`, `Value = WebServer-Prod`
* Used for billing, automation, and management.

---

## 💰 Pricing

EC2 pricing models:

| Model             | Description             | Example                        |
| ----------------- | ----------------------- | ------------------------------ |
| **On-Demand**     | Pay per hour/second     | Testing or short-term apps     |
| **Reserved**      | 1 or 3-year commitment  | Long-term predictable workload |
| **Spot**          | Bid for unused capacity | Batch jobs, flexible tasks     |
| **Savings Plans** | Flexible discount model | Commitment to consistent usage |

---

## 🧠 Practical Example

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

## ✅ Summary

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

```
