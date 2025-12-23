## 🌐 What is **AWS Site-to-Site VPN**?

**AWS Site-to-Site VPN** is a service that creates a **secure, encrypted connection** between your **on-premises network (office, data center)** and your **AWS Virtual Private Cloud (VPC)** over the **public internet** using **IPSec**.

Think of it as a **safe tunnel** between your company network and AWS.

---

### 🔐 How it works (Simple Flow)

1. You have an **on-premises network** (office/data center).
2. You create a **Virtual Private Gateway (VGW)** or **Transit Gateway** in AWS.
3. You configure a **Customer Gateway** (your router/firewall).
4. An **IPSec-encrypted tunnel** is established over the internet.
5. Data travels securely between on-prem and AWS.

---

### 🧱 Main Components

| Component                         | Meaning                     |
| --------------------------------- | --------------------------- |
| **VPC**                           | Your private network in AWS |
| **Virtual Private Gateway (VGW)** | AWS side of VPN             |
| **Customer Gateway (CGW)**        | Your office router/firewall |
| **VPN Tunnel**                    | Encrypted IPSec tunnel      |

---

### ✅ Key Features

* 🔒 **Encrypted using IPSec**
* 🌍 Uses **public internet**
* 🔁 Comes with **2 tunnels for high availability**
* 💰 **Low cost** compared to Direct Connect
* ⚡ Quick to set up

---

## 📌 Example 1: Office to AWS Connectivity

**Scenario:**
A company has an office in Bangalore and wants to access an **EC2 server** hosted in AWS.

**Solution:**

* Configure AWS Site-to-Site VPN
* Office employees can securely access:

  * EC2 instances
  * RDS databases
  * Internal applications

➡️ No need to expose services to the public internet.

---

## 📌 Example 2: Hybrid Cloud Setup

**Scenario:**
A company runs:

* Old applications on-prem
* New applications on AWS

**Solution:**

* Use Site-to-Site VPN
* Both environments communicate securely

➡️ On-prem app talks to AWS RDS as if it’s on the same network.

---

## 📌 Example 3: Backup & Disaster Recovery

**Scenario:**
Company wants to **backup on-prem data to AWS S3**.

**Solution:**

* Use Site-to-Site VPN
* Transfer backups securely to AWS

➡️ No public exposure, encrypted transfer.

---

### 🆚 Site-to-Site VPN vs Direct Connect

| Feature     | Site-to-Site VPN | Direct Connect         |
| ----------- | ---------------- | ---------------------- |
| Connection  | Internet         | Dedicated private line |
| Encryption  | Yes              | Optional               |
| Cost        | Low              | High                   |
| Setup time  | Fast             | Slow                   |
| Performance | Medium           | High                   |

---

### 🧠 When to Use AWS Site-to-Site VPN?

✔ Small to medium workloads
✔ Temporary or quick connectivity
✔ Backup connection for Direct Connect
✔ Cost-effective hybrid cloud

---

### 🔑 One-Line Summary

**AWS Site-to-Site VPN securely connects your on-premises network to AWS over the internet using IPSec encryption.**

