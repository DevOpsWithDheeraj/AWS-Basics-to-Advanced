
## What is Amazon DynamoDB?

**Amazon DynamoDB** is a **fully managed, serverless, NoSQL key-value and document database** service provided by AWS.
It is designed to deliver **single-digit millisecond performance at any scale**, with **high availability**, **automatic scaling**, and **built-in security**.

You don’t need to manage servers, operating systems, or database patching—AWS handles everything.

---

## Key Characteristics of DynamoDB

### 1. NoSQL Database

* Stores data as **key-value pairs** or **JSON documents**
* Schema-less (flexible structure)

### 2. Serverless

* No EC2, no infrastructure management
* Automatically scales up or down

### 3. High Performance

* Consistent **single-digit millisecond latency**
* Suitable for real-time applications

### 4. Highly Available & Durable

* Data automatically replicated across **multiple Availability Zones**
* Backed by **SSD storage**

### 5. Fully Managed

* Automatic backups
* Built-in monitoring (CloudWatch)
* Point-in-Time Recovery (PITR)

---

## Core Components of DynamoDB

### 1. Table

* Similar to a table in RDBMS
* Must have a **Primary Key**

### 2. Primary Key (Mandatory)

Two types:

1. **Partition Key** (Simple Primary Key)
2. **Partition Key + Sort Key** (Composite Primary Key)

### 3. Items

* A single row in a table
* Each item is uniquely identified by the primary key

### 4. Attributes

* Columns inside an item
* Can vary between items

---

## Example: Online Shopping Application

### Use Case

An **e-commerce application** storing customer orders.

---

### DynamoDB Table: `Orders`

#### Primary Key

* **Partition Key:** `CustomerId`
* **Sort Key:** `OrderId`

| CustomerId | OrderId | ProductName | Price | OrderDate  |
| ---------- | ------- | ----------- | ----- | ---------- |
| C101       | O1001   | Laptop      | 60000 | 2025-01-01 |
| C101       | O1002   | Mouse       | 800   | 2025-01-02 |
| C102       | O2001   | Mobile      | 30000 | 2025-01-03 |

---

### How Data is Accessed

#### Get all orders of a customer

```text
CustomerId = C101
```

➡ Returns all orders for that customer (very fast)

#### Get a specific order

```text
CustomerId = C101 AND OrderId = O1002
```

---

## DynamoDB vs RDBMS (Quick Comparison)

| Feature           | DynamoDB        | RDBMS           |
| ----------------- | --------------- | --------------- |
| Type              | NoSQL           | SQL             |
| Schema            | Flexible        | Fixed           |
| Scaling           | Automatic       | Manual          |
| Performance       | Milliseconds    | Slower at scale |
| Joins             | ❌ Not Supported | ✅ Supported     |
| Server Management | ❌ None          | ✅ Required      |

---

## Capacity Modes

### 1. Provisioned Capacity

* You specify **Read Capacity Units (RCU)** and **Write Capacity Units (WCU)**
* Cost-effective for predictable traffic

### 2. On-Demand Capacity

* Pay per request
* Best for unpredictable workloads

---

## Indexes in DynamoDB

### 1. Global Secondary Index (GSI)

* Query using non-primary key attributes

### 2. Local Secondary Index (LSI)

* Same partition key, different sort key

---

## Security Features

* IAM access control
* Encryption at rest (KMS)
* Encryption in transit (TLS)
* Fine-grained access using IAM policies

---

## Common Use Cases

* E-commerce platforms
* Gaming leaderboards
* IoT applications
* Session management
* Real-time analytics
* Mobile & web backends

---

## When NOT to Use DynamoDB

❌ Complex joins
❌ Highly relational data
❌ Strong ACID multi-table transactions (RDBMS is better)

---

## Real-World Example

**Amazon.com shopping cart**, **Netflix user profiles**, **Uber trip data** use DynamoDB-like NoSQL systems for speed and scalability.

---
