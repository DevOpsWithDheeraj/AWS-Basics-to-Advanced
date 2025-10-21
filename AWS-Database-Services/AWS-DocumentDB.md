# 📘 Amazon DocumentDB (with MongoDB Compatibility)

## 🧩 What is Amazon DocumentDB?

**Amazon DocumentDB** is a fully managed **document database service** designed to store, query, and index **JSON-like documents**.  
It is **compatible with MongoDB**, meaning that most MongoDB drivers, tools, and applications work seamlessly with DocumentDB without modification.

DocumentDB is ideal for use cases requiring **semi-structured data** storage — such as product catalogs, user profiles, content management systems, and mobile applications.

---

## ⚙️ Key Concepts

### 1. **Document-Oriented Model**
Instead of storing data in rows and columns like relational databases, DocumentDB stores data as **documents** (similar to JSON objects) in **collections**.

Example document:
```json
{
  "user_id": "U1001",
  "name": "John Doe",
  "email": "john@example.com",
  "address": { "city": "New York", "zip": "10001" },
  "purchases": ["Laptop", "Mouse", "Keyboard"]
}
````

### 2. **MongoDB Compatibility**

* Supports MongoDB **API versions 3.6, 4.0, and 5.0**.
* You can use **MongoDB tools** like `mongo shell`, `Compass`, or `Mongoose` (Node.js) with DocumentDB.
* Applications that work with MongoDB often work with DocumentDB **with little or no code change**.

### 3. **Managed Service**

AWS manages:

* **Backups**
* **Patching**
* **Monitoring**
* **Automatic failover**
* **Scalability**

You don’t need to manage underlying infrastructure.

---

## 🏗️ Architecture Overview

Amazon DocumentDB separates **storage** and **compute** layers:

* **Storage Layer (distributed & fault-tolerant):**

  * Automatically replicates six copies of your data across three Availability Zones.
  * Provides high durability and availability.

* **Compute Layer (instances):**

  * Your DocumentDB cluster can have **1 primary** (read/write) and **up to 15 replicas** (read-only).
  * Replicas can handle read traffic and automatically take over if the primary fails.

---

## 🚀 How It Works

1. **Create a Cluster**
   You start by creating a **DocumentDB cluster** (which contains your instances and storage volume).

2. **Connect Using MongoDB Drivers**
   Use your MongoDB connection string to connect your app to the cluster.

3. **Perform CRUD Operations**
   You can insert, update, delete, and query JSON documents using MongoDB APIs.

4. **Scale as Needed**

   * Increase the instance size or number of replicas.
   * The storage automatically scales up to 64 TB.

---

## 🧠 Features of Amazon DocumentDB

| Feature                    | Description                                                 |
| -------------------------- | ----------------------------------------------------------- |
| **MongoDB Compatibility**  | Works with MongoDB drivers and tools.                       |
| **Fully Managed**          | AWS handles operations like patching, backups, and scaling. |
| **Highly Available**       | Data replicated across 3 AZs automatically.                 |
| **Scalable Storage**       | Automatically scales up to 64 TB.                           |
| **Backup & Restore**       | Continuous backup to Amazon S3.                             |
| **Security**               | Integrated with AWS IAM, VPC, and KMS encryption.           |
| **Performance Monitoring** | Monitored using Amazon CloudWatch.                          |
| **Elastic Read Scaling**   | Add up to 15 read replicas.                                 |

---

## 💰 Pricing

Amazon DocumentDB pricing is based on:

1. **Instance Hours** – Cost per instance type (on-demand or reserved).
2. **Storage Usage** – Charged per GB-month.
3. **I/O Operations** – Per million requests.
4. **Backup Storage** – Beyond the database size.

📘 Example:
If you use a `db.r6g.large` instance for 10 hours and store 100 GB, you’ll pay for:

* 10 instance hours × hourly rate
* 100 GB storage × storage rate

Refer to [AWS Pricing Page](https://aws.amazon.com/documentdb/pricing/) for exact rates.

---

## 🔐 Security

* **Encryption at rest** using AWS KMS.
* **Encryption in transit** via TLS.
* **Network isolation** through Amazon VPC.
* **IAM policies** control access to cluster management.

---

## 🧰 Use Cases

1. **Content Management Systems** – Store articles, metadata, and tags.
2. **E-commerce Catalogs** – Store product info in flexible JSON format.
3. **User Profiles** – Handle variable attributes per user.
4. **Mobile or Gaming Apps** – Dynamic data models.
5. **IoT Data Storage** – Store unstructured device event data.

---

## 🧪 Practical Example — E-commerce Product Catalog

### 🎯 Goal:

Build a product catalog system using Amazon DocumentDB.

---

### **Step 1: Create a DocumentDB Cluster**

Go to **AWS Console → DocumentDB → Create Cluster**

* Engine: `Amazon DocumentDB (MongoDB compatibility)`
* Instance type: `db.r6g.large`
* Instances: 1 (for demo)
* Enable **encryption**, **backups**, and **VPC access**

Wait for the cluster to be “available”.

---

### **Step 2: Connect Using MongoDB Shell**

Use your connection string (from the AWS console):

```bash
mongo "mongodb://my-docdb-cluster.cluster-abcdefgh.us-east-1.docdb.amazonaws.com:27017" \
  --username myUser --password myPassword --tls
```

---

### **Step 3: Create Database and Collection**

```javascript
use ecommerce;
db.createCollection("products");
```

---

### **Step 4: Insert Documents**

```javascript
db.products.insertMany([
  {
    "product_id": "P001",
    "name": "Wireless Mouse",
    "category": "Electronics",
    "price": 25.99,
    "stock": 120,
    "features": { "color": "black", "connectivity": "Bluetooth" }
  },
  {
    "product_id": "P002",
    "name": "Gaming Keyboard",
    "category": "Electronics",
    "price": 89.99,
    "stock": 75,
    "features": { "backlight": "RGB", "switch": "Mechanical" }
  }
]);
```

---

### **Step 5: Query Data**

```javascript
db.products.find({ "category": "Electronics" }).pretty();
```

**Output:**

```json
{
  "product_id": "P001",
  "name": "Wireless Mouse",
  "price": 25.99
},
{
  "product_id": "P002",
  "name": "Gaming Keyboard",
  "price": 89.99
}
```

---

### **Step 6: Update and Delete**

```javascript
db.products.updateOne({ "product_id": "P001" }, { $set: { "stock": 110 } });
db.products.deleteOne({ "product_id": "P002" });
```

---

### **Step 7: Monitor and Scale**

Use **CloudWatch Metrics** to monitor:

* CPU utilization
* Read/Write IOPS
* Storage usage

Scale up the instance or add replicas as needed.

---

## 🧭 Best Practices

* Use **read replicas** for heavy read workloads.
* Enable **TLS encryption** for all connections.
* Use **parameter groups** for performance tuning.
* Schedule **automated backups** regularly.
* Isolate DocumentDB within a **private VPC**.
* Use **IAM roles** for controlled access.

---

## 🏁 Summary

| Feature           | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| **Type**          | Managed Document Database                                  |
| **Data Model**    | JSON-like Documents                                        |
| **Compatibility** | MongoDB API                                                |
| **Scalability**   | Up to 64 TB and 15 replicas                                |
| **Security**      | IAM, KMS, TLS, VPC                                         |
| **Best For**      | Flexible schema use cases like CMS, IoT, and User Profiles |

---

## 🧩 Final Thoughts

Amazon DocumentDB simplifies handling semi-structured JSON data at scale, without the administrative overhead of managing MongoDB clusters.
With its seamless MongoDB compatibility, managed scaling, and AWS ecosystem integration, it’s an ideal choice for cloud-native, flexible data storage needs.

---

**📚 Reference:**

* [Amazon DocumentDB Official Docs](https://docs.aws.amazon.com/documentdb/latest/developerguide/what-is.html)
* [AWS Pricing for DocumentDB](https://aws.amazon.com/documentdb/pricing/)


Would you like me to also create a downloadable `.md` file (`Amazon_DocumentDB_Guide.md`) for you?
```
