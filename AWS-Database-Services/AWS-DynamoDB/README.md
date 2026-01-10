

# 🌐 What is Amazon DynamoDB?

**Amazon DynamoDB** is a **fully managed, serverless, NoSQL key-value and document database** provided by AWS.

It is designed for:

* **High performance**
* **Massive scalability**
* **Single-digit millisecond latency**
* **Automatic scaling**

👉 AWS handles **servers, storage, replication, patching, and backups**.

---

# 🧠 Simple Definition (Layman Terms)

> DynamoDB is like a **super-fast table** where you can store and retrieve data instantly, and AWS automatically scales it for millions of users.

---

# 🗂️ DynamoDB Data Model

## 1️⃣ Tables

Similar to a table in RDBMS but **schema-less**.

## 2️⃣ Items

Each row = **Item**.

## 3️⃣ Attributes

Each column = **Attribute**.

---

# 🔑 Primary Key in DynamoDB

Every table **must have a primary key**.

## Types of Primary Keys:

### 🔹 Partition Key (Simple Key)

* Single attribute
* Used to distribute data

Example:

```
UserId = "U123"
```

---

### 🔹 Partition Key + Sort Key (Composite Key)

Example:

```
Partition Key: OrderId
Sort Key: OrderDate
```

Allows multiple items per partition.

---

# 🧪 Real-World Example (User Table)

### Table: `Users`

| UserId (PK) | Name    | Email                                         | Age |
| ----------- | ------- | --------------------------------------------- | --- |
| U101        | Dheeraj | [dheeraj@gmail.com](mailto:dheeraj@gmail.com) | 26  |
| U102        | Rahul   | [rahul@gmail.com](mailto:rahul@gmail.com)     | 25  |

📌 `UserId` is the **Partition Key**.

---

# ⚡ Performance: RCU & WCU

## 🔹 Read Capacity Unit (RCU)

* 1 RCU = 1 strongly consistent read (4 KB)
* Or 2 eventually consistent reads (4 KB)

## 🔹 Write Capacity Unit (WCU)

* 1 WCU = 1 write per second (1 KB)

---

# 🔁 Consistency Models

| Type                      | Description        |
| ------------------------- | ------------------ |
| **Eventually Consistent** | Faster, default    |
| **Strongly Consistent**   | Always latest data |

---

# 📊 Query vs Scan

| Feature     | Query | Scan |
| ----------- | ----- | ---- |
| Uses PK     | Yes   | No   |
| Performance | Fast  | Slow |
| Cost        | Low   | High |

---

# 📌 Indexes in DynamoDB

## 🔹 Global Secondary Index (GSI)

* Different partition key
* Can query on non-primary attributes

## 🔹 Local Secondary Index (LSI)

* Same partition key
* Different sort key

---

# 🔐 Security in DynamoDB

* IAM policies
* VPC endpoints
* Encryption at rest (KMS)
* TLS encryption in transit

---

# 🔄 Backup & Recovery

| Feature                       | Description                        |
| ----------------------------- | ---------------------------------- |
| On-Demand Backup              | Manual                             |
| Point-in-Time Recovery (PITR) | Restore any second in last 35 days |

---

# 🌍 Global Tables

* Multi-region replication
* Active-Active setup
* Low latency worldwide

Example:

* Region 1: Mumbai
* Region 2: Virginia
* Automatic sync

---

# 💰 DynamoDB Pricing

You pay for:

* Read/Write capacity
* Storage
* On-demand requests
* Streams & backups

### Capacity Modes:

| Mode        | Use Case              |
| ----------- | --------------------- |
| Provisioned | Predictable traffic   |
| On-Demand   | Unpredictable traffic |

---

# 🧪 Real-World Example (E-commerce Orders)

### Table: `Orders`

| OrderId (PK) | OrderDate (SK) | UserId | Amount |
| ------------ | -------------- | ------ | ------ |
| O101         | 2024-01-01     | U101   | 2500   |
| O101         | 2024-01-02     | U101   | 3000   |

✔️ Query orders by OrderId
✔️ Fast performance
✔️ Scales automatically

---

# 🆚 DynamoDB vs RDS

| Feature     | DynamoDB     | RDS        |
| ----------- | ------------ | ---------- |
| Type        | NoSQL        | Relational |
| Schema      | Schema-less  | Fixed      |
| Scaling     | Automatic    | Manual     |
| Joins       | ❌            | ✅          |
| Performance | Milliseconds | Slower     |

---

# ❌ Limitations of DynamoDB

* No joins
* No complex SQL
* Item size limit: **400 KB**
* Learning curve for key design

---

# 🎯 When to Use DynamoDB?

✅ Use when:

* Massive scale required
* Low latency needed
* Serverless apps
* IoT, gaming, real-time apps

❌ Avoid when:

* Complex joins needed
* Heavy relational queries

---

# 📌 One-Line Interview Answer

> **Amazon DynamoDB is a fully managed, serverless NoSQL database that provides fast and predictable performance with seamless scalability.**

---
