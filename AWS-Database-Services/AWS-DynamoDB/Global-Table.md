
## What is DynamoDB Global Table?

**DynamoDB Global Tables** allow you to **replicate a DynamoDB table automatically across multiple AWS Regions**.

👉 It provides:

* **Multi-Region, fully managed replication**
* **Low latency** for global users
* **High availability & disaster recovery**
* **Active-Active architecture** (read/write in all regions)

In short:

> **Same table, same data, multiple regions – automatically synced**

---

## What is Cross-Region Replication in DynamoDB?

Cross-region replication means:

* When data is **written/updated/deleted in one region**,
* DynamoDB **automatically replicates** that change to all other regions in the Global Table.

This replication is:

* **Asynchronous**
* **Eventually consistent across regions**
* **Automatic** (no Lambda, no streams, no custom code)

---

## Architecture Overview

```
User (India) → DynamoDB (ap-south-1)
                    ↓
            Automatic Replication
                    ↓
User (US)   → DynamoDB (us-east-1)
```

✔ Both regions have **read & write access**
✔ Data stays **in sync**

---

## Example 1: Global E-Commerce Application 🌍

### Scenario

You run an **e-commerce app** with users in:

* India
* USA
* Europe

### Regions

* ap-south-1 (Mumbai)
* us-east-1 (N. Virginia)
* eu-west-1 (Ireland)

### Table

`Orders`

**Partition Key:** `OrderId`

---

### Step 1: Create Global Table

Create DynamoDB table `Orders` in:

* ap-south-1
* us-east-1
* eu-west-1

Enable **Global Table replication**.

---

### Step 2: Write Data in One Region

User in India places an order:

```json
{
  "OrderId": "ORD101",
  "UserId": "U123",
  "Amount": 5000,
  "Status": "PLACED"
}
```

📍 Written to **ap-south-1**

---

### Step 3: Automatic Replication

DynamoDB replicates this record to:

* us-east-1
* eu-west-1

✅ No manual sync
✅ No code required

---

### Step 4: Read from Another Region

User in USA queries `OrderId = ORD101`

📍 Reads from **us-east-1**

✔ Low latency
✔ Same data

---

## Example 2: Disaster Recovery (DR) Use Case 🔥

### Scenario

Primary region **ap-south-1** goes down.

### What happens?

* Application automatically switches to **us-east-1**
* Data is already available
* No restore required

💡 **RTO ≈ seconds**
💡 **RPO ≈ seconds**

---

## Conflict Resolution in Global Tables ⚠️

Since **multiple regions can write**, conflicts can happen.

### DynamoDB uses:

### 👉 **Last Writer Wins (LWW)**

Based on:

* **Timestamp**
* **Region-specific version**

---

### Conflict Example

| Region | Status Update | Time  |
| ------ | ------------- | ----- |
| India  | SHIPPED       | 10:00 |
| USA    | CANCELLED     | 10:01 |

✅ **CANCELLED wins** (latest timestamp)

---

## Consistency Model

| Scope        | Consistency                    |
| ------------ | ------------------------------ |
| Same Region  | Strong or Eventual             |
| Cross Region | **Eventually Consistent only** |

❌ Strong consistency across regions is **NOT supported**

---

## Pricing Considerations 💰

You pay for:

* **Write requests** (replicated to all regions)
* **Read requests per region**
* **Data transfer between regions**

⚠ Write in 1 region = write in **N regions**

---

## When to Use DynamoDB Global Tables?

✅ Global applications
✅ Multi-region active-active apps
✅ Disaster recovery
✅ Low-latency worldwide access

---

## When NOT to Use?

❌ Strong cross-region consistency required
❌ High write volume with tight cost limits
❌ Single-region applications

---

## Key Interview Summary 🚀

> **DynamoDB Global Tables provide fully managed, active-active, cross-region replication with eventual consistency, enabling low-latency global access and disaster recovery without custom replication logic.**

---
