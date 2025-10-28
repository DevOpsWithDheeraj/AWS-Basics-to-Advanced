## 🌐 What is a Network ACL (NACL)?

A **Network Access Control List (NACL)** is a **stateless firewall** that controls **inbound and outbound traffic** **at the subnet level** in an **AWS VPC**.

Think of it like the **security gate of a neighborhood** (subnet) —
it decides which cars (network packets) can **enter or leave** that neighborhood.

---

## ⚙️ Key Characteristics of NACLs

| Feature          | Description                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| **Level**        | Works at the **subnet level** (affects all instances in that subnet).                                   |
| **Stateless**    | Responses to allowed inbound traffic **must be explicitly allowed** in outbound rules (and vice versa). |
| **Rule-Based**   | Rules are processed **in numerical order** — the first matching rule decides the outcome.               |
| **Allow / Deny** | NACLs can both **allow** and **deny** traffic (unlike Security Groups, which only allow).               |
| **Default NACL** | Every VPC automatically has a default NACL (allows all inbound/outbound traffic).                       |
| **Custom NACL**  | Starts with **deny all traffic** by default until you add rules.                                        |
| **Association**  | Each subnet can be associated with **only one NACL** at a time.                                         |

---

## 🧩 How NACLs Work (Traffic Flow)

Let’s imagine:

* VPC: `10.0.0.0/16`
* Public Subnet: `10.0.1.0/24`
* Private Subnet: `10.0.2.0/24`

### 1️⃣ Inbound Traffic

When a packet enters a subnet (e.g., from the Internet or another subnet),
the **Inbound Rules** of the subnet’s NACL are evaluated.

### 2️⃣ Outbound Traffic

When a packet leaves a subnet (e.g., EC2 sending data out),
the **Outbound Rules** are evaluated.

Both inbound and outbound must be explicitly allowed for the flow to succeed.
If no rule matches → **“Deny” by default.**

---

## 🧠 Example NACL Configuration

| Rule #  | Type     | Protocol | Port Range | Source/Destination | Allow/Deny |
| ------- | -------- | -------- | ---------- | ------------------ | ---------- |
| **100** | Inbound  | TCP      | 80         | 0.0.0.0/0          | ALLOW      |
| **110** | Inbound  | TCP      | 22         | 0.0.0.0/0          | ALLOW      |
| **120** | Inbound  | ALL      | ALL        | 0.0.0.0/0          | DENY       |
| **100** | Outbound | TCP      | 1024–65535 | 0.0.0.0/0          | ALLOW      |
| **110** | Outbound | ALL      | ALL        | 0.0.0.0/0          | DENY       |

🔹 Rule processing is **top-down** — once a rule matches, later ones are ignored.
🔹 The **lowest numbered rule** has the **highest priority**.

---

## 🧩 Example Flow: HTTP Traffic

A user accesses your EC2 web server:

1. Request from Internet enters subnet → inbound rule #100 (port 80 ALLOW).
2. Response leaves subnet → outbound rule #100 (ephemeral ports 1024–65535 ALLOW).
   ✅ Connection successful.

If outbound rule didn’t allow ephemeral ports,
the **response would be blocked**, because NACLs are stateless.

---

## 🧱 Default vs Custom NACLs

| Feature                   | Default NACL               | Custom NACL                     |
| ------------------------- | -------------------------- | ------------------------------- |
| **Inbound Rules**         | Allows all                 | Denies all                      |
| **Outbound Rules**        | Allows all                 | Denies all                      |
| **Associated By Default** | New subnets                | Only if manually associated     |
| **Rule Modification**     | Can be edited              | Can be created from scratch     |
| **Recommended Use**       | For testing or open access | For production (tight security) |

---

## 🏗️ Example Architecture

```
            Internet
                │
         ┌──────────────┐
         │ Internet GW  │
         └──────────────┘
                │
      ┌───────────────────────┐
      │   Public Subnet       │
      │   10.0.1.0/24         │
      │   NACL: ALLOW 80/22   │
      │   EC2: Web Server     │
      └───────────────────────┘
                │
      ┌───────────────────────┐
      │   Private Subnet      │
      │   10.0.2.0/24         │
      │   NACL: Allow 3306    │
      │   EC2: Database       │
      └───────────────────────┘
```

* Public Subnet NACL allows HTTP (80) and SSH (22) from anywhere.
* Private Subnet NACL allows MySQL (3306) **only from 10.0.1.0/24**.

✅ This isolates the database, allowing access only from web servers.

---

## 🔄 Order of Packet Evaluation in AWS Networking

1. **Route Table** → Determines next hop.
2. **Network ACL** → Checks subnet-level access.
3. **Security Group** → Checks instance-level access.

If any layer denies traffic → packet is dropped.

---

## 🔒 Security Best Practices

✅ Use **NACLs for broad subnet-level filtering** (e.g., allow HTTP only to web tier).
✅ Use **Security Groups for finer control** at instance level.
✅ Always include **ephemeral port ranges (1024–65535)** for outbound return traffic.
✅ Assign different NACLs to public and private subnets.
✅ Keep rule numbers spaced (e.g., 100, 110, 120) to allow future additions.
✅ Log and monitor with **VPC Flow Logs**.

---

## 🧾 Quick Summary Table

| Concept              | Description                                                                   |
| -------------------- | ----------------------------------------------------------------------------- |
| **Definition**       | Stateless firewall that filters inbound/outbound traffic at the subnet level. |
| **Default Behavior** | Default NACL allows all; custom NACL denies all until rules added.            |
| **Rule Processing**  | Evaluated in ascending order — first match wins.                              |
| **Directionality**   | Separate rules for inbound and outbound.                                      |
| **Statefulness**     | Stateless — responses must be explicitly allowed.                             |
| **Association**      | One NACL per subnet.                                                          |
| **Control Level**    | Subnet-level (affects all instances in subnet).                               |
| **Logging**          | Integrated with VPC Flow Logs for monitoring.                                 |

---

## 💡 Real-World Analogy

Imagine:

* **NACLs** = the **security gate at a housing colony** — checks vehicles entering or exiting the entire neighborhood (subnet).
* **Security Groups** = the **locks on individual houses** (instances).

Together, they create **defense in depth** 🔐.

---
