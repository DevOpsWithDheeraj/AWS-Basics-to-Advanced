## 🔗 What is **VPC Peering** (AWS)?

**VPC Peering** is a networking feature in AWS that allows **two Virtual Private Clouds (VPCs)** to **communicate with each other privately** using AWS’s internal network.

Think of it as a **private bridge** between two VPCs 🛣️.

---

## 📘 Simple Definition

> **VPC Peering** enables private connectivity between two VPCs so that resources (EC2, RDS, Lambda, etc.) can communicate using **private IP addresses**.

---

## 🧠 Key Characteristics

✅ **Private communication** (no internet required)
✅ **Low latency & high bandwidth**
✅ **One-to-one connection only**
❌ **No transitive routing**
❌ **Overlapping CIDR blocks not allowed**

---

## 🏗️ Types of VPC Peering

1. **Intra-Region Peering**

   * Between VPCs in the **same region**

2. **Inter-Region Peering**

   * Between VPCs in **different regions**

3. **Cross-Account Peering**

   * Between VPCs in **different AWS accounts**

---

## 🔁 How VPC Peering Works (Steps)

1. Create a **VPC peering request**
2. Accept the request from the other VPC
3. Update **route tables** in both VPCs
4. Configure **Security Groups / NACLs**
5. Start communication 🎉

---

## 📌 Example (Real-World)

### 🏢 Scenario:

* **VPC A (10.0.0.0/16)** → Application servers
* **VPC B (10.1.0.0/16)** → Database servers

You want the app in VPC A to access the DB in VPC B **securely**.

👉 Create **VPC Peering** between VPC A and VPC B
👉 Add routes:

* VPC A → 10.1.0.0/16 via Peering
* VPC B → 10.0.0.0/16 via Peering

Now the app can talk to the DB using **private IPs** 🔐

---

## 🚫 Limitations (Important for Exams)

❌ No **transitive peering**

```
VPC A ↔ VPC B ↔ VPC C
A ❌ cannot talk to C
```

❌ Cannot peer VPCs with **overlapping CIDR**

❌ No centralized hub-and-spoke model

👉 For large networks → **Transit Gateway** is better

---

## 🆚 VPC Peering vs Transit Gateway

| Feature            | VPC Peering       | Transit Gateway       |
| ------------------ | ----------------- | --------------------- |
| Connections        | One-to-one        | Hub-and-spoke         |
| Transitive routing | ❌ No              | ✅ Yes                 |
| Scalability        | Limited           | Highly scalable       |
| Use case           | Simple VPC-to-VPC | Enterprise networking |

---

## 🎯 When to Use VPC Peering?

✔ Simple connectivity
✔ Few VPCs
✔ Low cost & low complexity
✔ No need for transitive routing

---
