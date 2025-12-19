
## 🌍 What is AWS Global Infrastructure?

AWS Global Infrastructure is the **worldwide network of data centers** that AWS uses to deliver cloud services with **high availability, low latency, scalability, and fault tolerance**.

It is made up of:

1. **Regions**
2. **Availability Zones (AZs)**
3. **Edge Locations**
4. **Local Zones** (optional, near large cities)

---

## 🧱 Core Components :

### 1️⃣ AWS Regions

* A **Region** is a **geographical area**.
* Each Region is completely **independent** from others.
* Used for **data residency, latency, and compliance**.

📌 Example:
If your users are in India, you deploy EC2 in **ap-south-1 (Mumbai)** to reduce latency.

---

### 2️⃣ Availability Zones (AZs)

* Each Region has **multiple AZs**.
* An AZ is **one or more data centers** with:

  * Independent power
  * Independent networking
* AZs are connected with **high-speed, low-latency private links**.

📌 Example:
You deploy:

* EC2 in **AZ-A**
* RDS replica in **AZ-B**

If AZ-A fails, traffic shifts to AZ-B → **High Availability**.

---

### 3️⃣ Edge Locations

* Used by **Amazon CloudFront (CDN)**.
* Cache content closer to users for **faster delivery**.
* Not used to deploy EC2.

📌 Example:
A user in Delhi accesses your website.
Content is served from **Delhi Edge Location**, not Mumbai → faster load.

---

### 4️⃣ Local Zones

* Extend an AWS Region **closer to large metro cities**.
* Used for **ultra-low latency workloads** (gaming, media, real-time apps).

📌 Example:
You host a gaming backend in **Delhi Local Zone** instead of Mumbai.

---

## 🇮🇳 AWS Global Infrastructure in India (Names & Numbers)

### ✅ AWS Regions in India

| Region Name | Region Code  |
| ----------- | ------------ |
| Mumbai      | `ap-south-1` |
| Hyderabad   | `ap-south-2` |

➡ **Total Regions in India: 2**

---

### ✅ Availability Zones in India

| Region                   | Number of AZs |
| ------------------------ | ------------- |
| Mumbai (`ap-south-1`)    | 3 AZs         |
| Hyderabad (`ap-south-2`) | 3 AZs         |

➡ **Total AZs in India: 6**

---

### ✅ Edge Locations in India (Major Cities)

AWS has **multiple Edge Locations** across India, including:

* Mumbai
* Delhi
* Chennai
* Bengaluru
* Hyderabad
* Kolkata
* Pune

➡ Used mainly by **CloudFront, Route 53, Shield, WAF**

*(Exact count may change, but India has **many active edge locations**)*

---

### ✅ AWS Local Zones in India

| City    | Parent Region         |
| ------- | --------------------- |
| Delhi   | Mumbai (`ap-south-1`) |
| Chennai | Mumbai (`ap-south-1`) |

➡ Used for **latency-sensitive workloads**

---

## 📌 One-Line Summary (Interview Ready)

> AWS Global Infrastructure consists of **Regions**, **Availability Zones**, **Edge Locations**, and **Local Zones**, enabling applications to be **highly available, fault-tolerant, and low-latency worldwide**.

