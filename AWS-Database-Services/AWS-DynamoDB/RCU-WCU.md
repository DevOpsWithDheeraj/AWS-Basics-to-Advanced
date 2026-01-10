
## 1️⃣ What is Capacity in DynamoDB?

Capacity defines **how much data DynamoDB can read or write per second** for a table.

There are **two kinds of capacity**:

* **Read Capacity**
* **Write Capacity**

And **two capacity modes**:

* **Provisioned Capacity**
* **On-Demand Capacity**

---

# 🔹 READ CAPACITY (RCU – Read Capacity Unit)

Read capacity controls **how many reads per second** your table can handle.

### 🔸 What is 1 RCU?

* **1 RCU =**

  * **1 strongly consistent read** of **up to 4 KB**, OR
  * **2 eventually consistent reads** of **up to 4 KB**

---

## 📘 Types of Read Consistency

### 1️⃣ Strongly Consistent Read

* Always returns **latest data**
* Uses **more capacity**
* Default in DynamoDB **Query & GetItem**

**Example:**

* Item size = **4 KB**
* 1 strongly consistent read/sec
  👉 Requires **1 RCU**

---

### 2️⃣ Eventually Consistent Read

* Data may be **slightly outdated** (few milliseconds)
* Uses **half the capacity**
* Default for **Scan operations**

**Example:**

* Item size = **4 KB**
* 2 reads/sec
  👉 Requires **1 RCU**

---

### 🔢 Read Capacity Calculation Example

**Scenario:**

* Item size = **8 KB**
* Strongly consistent reads
* 10 reads/sec

**Calculation:**

* 8 KB = **2 × 4 KB**
* Each read = **2 RCUs**
* 10 reads/sec = **20 RCUs**

---

# 🔹 WRITE CAPACITY (WCU – Write Capacity Unit)

Write capacity controls **how many writes per second** DynamoDB supports.

### 🔸 What is 1 WCU?

* **1 WCU = 1 write per second of up to 1 KB**

---

## ✍️ Write Capacity Examples

### Example 1: Small Item

* Item size = **1 KB**
* Writes/sec = **5**

👉 Required **5 WCUs**

---

### Example 2: Large Item

* Item size = **3 KB**
* Writes/sec = **10**

**Calculation:**

* 3 KB = **3 WCUs per write**
* 10 writes/sec = **30 WCUs**

---

### ⚠️ Important Note

* Writes are **always strongly consistent**
* Applies to:

  * `PutItem`
  * `UpdateItem`
  * `DeleteItem`

---

# 🔹 DynamoDB Capacity Modes (Types)

## 1️⃣ Provisioned Capacity Mode

You **manually specify RCUs & WCUs**.

### ✅ Features:

* Predictable traffic
* Lower cost for steady workloads
* Auto Scaling available

### 📘 Example:

* RCUs = 100
* WCUs = 50
  👉 DynamoDB supports:
* 100 strongly consistent reads/sec
* 50 writes/sec (1 KB items)

---

## 2️⃣ On-Demand Capacity Mode

AWS **automatically handles capacity**.

### ✅ Features:

* No planning required
* Best for unpredictable traffic
* Pay per request

### 📘 Example:

* Sudden spike from 100 → 10,000 requests/sec
  👉 DynamoDB scales automatically without throttling

---

# 🔄 Comparison Table

| Feature           | Provisioned              | On-Demand       |
| ----------------- | ------------------------ | --------------- |
| Capacity planning | Required                 | Not required    |
| Cost              | Cheaper (steady traffic) | Higher          |
| Auto scaling      | Optional                 | Built-in        |
| Best for          | Predictable apps         | Spiky workloads |

---

# 🎯 Real-World Use Case Example

### 🛒 E-commerce Website

* Product catalog → **Eventually consistent reads**
* Orders & payments → **Strongly consistent reads**
* Flash sales → **On-Demand capacity**
* Regular traffic → **Provisioned capacity with Auto Scaling**

---

# 🧠 Interview Summary (One-Liner)

> **RCU controls read throughput (4 KB per unit), WCU controls write throughput (1 KB per unit). DynamoDB offers Provisioned and On-Demand capacity modes depending on traffic predictability.**

---
