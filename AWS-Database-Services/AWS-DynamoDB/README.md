# 🟢 **Amazon DynamoDB Overview**

**Amazon DynamoDB** is a **fully managed NoSQL database service** offered by AWS.
It provides **fast and predictable performance** with **seamless scalability**.

It’s ideal for applications that need **consistent, single-digit millisecond latency** — such as **real-time analytics, IoT, gaming, e-commerce**, and **serverless apps**.

---

## ⚙️ 1. **Key Features**

| Feature                 | Description                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------- |
| **NoSQL Database**      | Stores data as *key-value* and *document-based* instead of rows and columns.          |
| **Fully Managed**       | AWS handles provisioning, patching, scaling, and replication.                         |
| **Auto Scaling**        | Automatically adjusts read/write capacity based on traffic.                           |
| **Serverless**          | No need to manage servers or infrastructure.                                          |
| **High Availability**   | Data is replicated across multiple AZs in a region.                                   |
| **Integrated Security** | Supports IAM, encryption at rest (KMS), and network isolation (VPC).                  |
| **Streams**             | Captures item-level changes in near real-time (useful for event-driven architecture). |

---

## 🧩 2. **Core Components**

| Component                    | Description                                                                           |
| ---------------------------- | ------------------------------------------------------------------------------------- |
| **Table**                    | Collection of items (like a table in SQL).                                            |
| **Item**                     | A single record (like a row in SQL).                                                  |
| **Attribute**                | A field or column in the item.                                                        |
| **Primary Key**              | Uniquely identifies each item in a table.                                             |
| **Partition Key (Hash Key)** | Used to distribute data across partitions.                                            |
| **Sort Key (Range Key)**     | Optional — allows multiple items with the same partition key but different sort keys. |

---

## 📘 3. **Example 1: Simple DynamoDB Table**

Let’s say we are building a **user profile service** for an application.

**Table Name:** `Users`
**Primary Key:** `UserID` (Partition Key)

| UserID | Name    | Email                                     | Age | City      |
| ------ | ------- | ----------------------------------------- | --- | --------- |
| 101    | Dheeraj | [dheeraj@xyz.com](mailto:dheeraj@xyz.com) | 26  | Pune      |
| 102    | Rahul   | [rahul@abc.com](mailto:rahul@abc.com)     | 29  | Bengaluru |
| 103    | Mansi   | [mansi@pqr.com](mailto:mansi@pqr.com)     | 25  | Delhi     |

Here:

* Each item (row) represents a user.
* Each attribute (column) stores user details.
* `UserID` is the **partition key**, which ensures uniqueness.

---

## 📘 **Example 2: Table with Sort Key**

If you want to store **multiple orders per customer**, you can use a **composite primary key** (Partition + Sort Key).

**Table Name:** `Orders`
**Partition Key:** `CustomerID`
**Sort Key:** `OrderID`

| CustomerID | OrderID | Date       | Amount | Status  |
| ---------- | ------- | ---------- | ------ | ------- |
| 101        | O-001   | 2025-10-30 | 5000   | Shipped |
| 101        | O-002   | 2025-10-31 | 2000   | Pending |
| 102        | O-001   | 2025-10-31 | 3000   | Shipped |

Now you can:

* Retrieve **all orders for CustomerID = 101** quickly.
* Sort orders by `OrderID` or `Date`.

---

## ⚡ 4. **Access Patterns**

### Example Queries:

```python
# Using boto3 (Python AWS SDK)
import boto3
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')

# Get item
response = table.get_item(Key={'UserID': 101})
print(response['Item'])

# Put item
table.put_item(Item={
    'UserID': 104,
    'Name': 'Ravi',
    'Email': 'ravi@xyz.com',
    'Age': 28,
    'City': 'Mumbai'
})
```

---

## 🧠 5. **DynamoDB Streams Example**

You can enable **Streams** to capture changes in a table and trigger a **Lambda function** automatically.

📍 Example use case:
Whenever a new order is added to the `Orders` table → A Lambda function sends an email confirmation.

---

## 🔄 6. **Use Cases**

| Use Case                | Description                                   |
| ----------------------- | --------------------------------------------- |
| **E-commerce Cart**     | Store user carts and order history.           |
| **IoT Applications**    | Store sensor data with high throughput.       |
| **Gaming Leaderboards** | Store player scores in real-time.             |
| **Serverless Apps**     | Works seamlessly with Lambda + API Gateway.   |
| **Session Management**  | Store and retrieve user sessions efficiently. |

---

## 📊 7. **Comparison with RDS**

| Feature    | DynamoDB                      | RDS                            |
| ---------- | ----------------------------- | ------------------------------ |
| Data Model | NoSQL (key-value, document)   | Relational (tables, rows, SQL) |
| Scaling    | Automatic                     | Manual or Read Replica         |
| Schema     | Flexible                      | Fixed schema                   |
| Query Type | Key-based                     | SQL Queries                    |
| Ideal For  | High scale, unstructured data | Structured data, transactions  |

---

## 🚀 8. **Example Real-world Scenario**

Let’s say your **e-commerce app** uses:

* **Frontend:** React
* **Backend:** AWS Lambda + API Gateway
* **Database:** DynamoDB (stores orders and inventory)

When a user places an order:

1. API Gateway receives the request.
2. Lambda function validates and stores order data in DynamoDB.
3. DynamoDB Stream triggers another Lambda to update stock or send confirmation.

👉 This makes the app **serverless**, **scalable**, and **low-latency**.

---
