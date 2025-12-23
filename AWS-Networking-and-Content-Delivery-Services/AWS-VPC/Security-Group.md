### 🔐 What is a **Security Group** (in AWS)?

A **Security Group (SG)** is a **virtual firewall** in AWS that **controls inbound and outbound traffic** for AWS resources like **EC2 instances, RDS, ALB, Lambda (VPC)**, etc.

Think of it as a **security guard at the door** that decides **who is allowed in and out**.

---

## ⭐ Key Characteristics of Security Groups

1. **Stateful**

   * If **inbound traffic is allowed**, the **response traffic is automatically allowed** (no need to add outbound rules separately).

2. **Allows rules only**

   * Security Groups **only allow traffic** (❌ no explicit deny rules).

3. **Instance-level**

   * Applied directly to **EC2 instances** or other resources.

4. **Evaluated before traffic reaches the instance**

   * Acts as the **first line of defense**.

---

## 📥 Inbound Rules (Who can access?)

Example:

| Type  | Protocol | Port | Source    |
| ----- | -------- | ---- | --------- |
| SSH   | TCP      | 22   | My IP     |
| HTTP  | TCP      | 80   | 0.0.0.0/0 |
| HTTPS | TCP      | 443  | 0.0.0.0/0 |

✔ Allows SSH only from your laptop
✔ Allows web traffic from the internet

---

## 📤 Outbound Rules (Where can it go?)

By default:

* **All outbound traffic is allowed**

Example:

| Type        | Protocol | Port | Destination |
| ----------- | -------- | ---- | ----------- |
| All traffic | All      | All  | 0.0.0.0/0   |

---

## 🧠 Simple Real-World Example

You have an **EC2 web server**:

* Users should access the website → **Allow port 80/443**
* Only you should SSH → **Allow port 22 from your IP**
* Block everything else → **Automatically blocked**

➡ This is done using a **Security Group**.

---

## 🆚 Security Group vs NACL (Quick Comparison)

| Feature    | Security Group | NACL          |
| ---------- | -------------- | ------------- |
| Level      | Instance level | Subnet level  |
| Stateful   | ✅ Yes          | ❌ No          |
| Allow/Deny | Allow only     | Allow & Deny  |
| Default    | Deny inbound   | Allow inbound |

---

## ✅ When to Use Security Groups

* Protect **EC2, RDS, ALB**
* Control **application-level access**
* Follow **least privilege** security model

---
