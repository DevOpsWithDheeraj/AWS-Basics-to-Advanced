

## **1. Choosing the Right Relational Database**

A startup is building an **e-commerce application** that requires:

* ACID-compliant transactions
* High availability
* Automated backups and patching

The database should be **fully managed** and **cost-effective**.

**Which AWS service should the Solutions Architect recommend?**

A. Amazon EC2 with MySQL installed manually <br>
B. Amazon RDS for MySQL <br>
C. Amazon DynamoDB <br>
D. Amazon Aurora Serverless v2 <br>

✅ **Correct Answer: B**

**Explanation:**
Amazon RDS for MySQL is a **fully managed relational database** that supports ACID transactions, automatic backups, patching, and Multi-AZ deployments. It is cost-effective compared to Aurora and easier to manage than EC2-hosted databases.

---

## **2. High Availability with Minimal Downtime**

A financial application uses **Amazon RDS (MySQL)** and requires:

* Automatic failover
* Minimal downtime during failures
* No manual intervention

**What should be configured?**

A. Read Replicas <br>
B. Manual snapshots <br>
C. Multi-AZ deployment <br>
D. Cross-Region replication <br>

✅ **Correct Answer: C**

**Explanation:**
**Multi-AZ** provides synchronous replication to a standby instance and supports **automatic failover**, ensuring high availability with minimal downtime.

---

## **3. Read-Heavy Workload Optimization**

An online news platform experiences:

* Very high read traffic
* Moderate write traffic

The team wants to **improve read performance** without affecting the primary database.

**What is the BEST solution?**

A. Enable Multi-AZ <br>
B. Use Amazon Aurora Global Database <br>
C. Create Read Replicas <br>
D. Increase instance size <br>

✅ **Correct Answer: C**

**Explanation:**
**Read Replicas** allow scaling read traffic independently from write operations. Multi-AZ is for availability, not performance.

---

## **4. Serverless Database Requirement**

A development team wants a database that:

* Automatically scales capacity
* Charges only for usage
* Requires no infrastructure management

The application uses a **relational schema**.

**Which service should be used?**

A. Amazon DynamoDB <br>
B. Amazon RDS MySQL <br>
C. Amazon Aurora Serverless v2 <br>
D. Amazon Redshift <br>

✅ **Correct Answer: C**

**Explanation:**
**Aurora Serverless v2** is a serverless relational database that automatically scales capacity and charges based on usage, ideal for unpredictable workloads.

---

## **5. Key-Value Store with Single-Digit Millisecond Latency**

A gaming application needs:

* Extremely low latency
* Automatic scaling
* NoSQL key-value data model

**Which database should be selected?**

A. Amazon RDS PostgreSQL <br>
B. Amazon Aurora <br>
C. Amazon DynamoDB <br>
D. Amazon ElastiCache Redis <br>

✅ **Correct Answer: C**

**Explanation:**
**DynamoDB** is a fully managed NoSQL key-value database designed for **single-digit millisecond latency** at any scale.

---

## **6. In-Memory Caching for Faster Performance**

An application frequently queries the same data, causing high load on the primary database.

**What is the MOST efficient way to reduce database load?**

A. Add more RDS Read Replicas <br>
B. Use Amazon ElastiCache <br>
C. Enable Multi-AZ <br>
D. Increase storage size <br>

✅ **Correct Answer: B**

**Explanation:**
**Amazon ElastiCache (Redis or Memcached)** provides in-memory caching, drastically reducing latency and database load.

---

## **7. Data Warehouse for Analytics**

A company wants to analyze **terabytes of historical data** using complex SQL queries and BI tools.

**Which AWS service is MOST appropriate?**

A. Amazon RDS <br>
B. Amazon DynamoDB <br>
C. Amazon Redshift <br>
D. Amazon Aurora <br>

✅ **Correct Answer: C**

**Explanation:**
**Amazon Redshift** is a fully managed **data warehouse** optimized for large-scale analytics and OLAP workloads.

---

## **8. Cross-Region Disaster Recovery**

A global application uses **Amazon Aurora** and needs:

* Low-latency global reads
* Fast disaster recovery across regions

**Which solution meets these requirements?**

A. Aurora Multi-AZ <br>
B. Aurora Read Replicas <br>
C. Aurora Global Database <br>
D. DynamoDB Global Tables <br>

✅ **Correct Answer: C**

**Explanation:**
**Aurora Global Database** enables cross-region replication with low-latency reads and rapid disaster recovery.

---

## **9. Automatic Backups and Point-in-Time Recovery**

Which AWS database service **automatically** provides point-in-time recovery (PITR)?

A. Amazon EC2 with MongoDB <br>
B. Amazon RDS <br>
C. Amazon S3 <br>
D. Amazon Redshift Spectrum <br>

✅ **Correct Answer: B**

**Explanation:**
**Amazon RDS** supports automatic backups and **point-in-time recovery** within the retention period.

---

## **10. NoSQL with Global Active-Active Access**

A mobile app requires:

* Low latency worldwide
* Multi-Region writes
* Automatic conflict resolution

**Which service should be used?**

A. Amazon Aurora Global Database <br>
B. Amazon DynamoDB Global Tables <br>
C. Amazon RDS Read Replicas <br>
D. Amazon ElastiCache <br>

✅ **Correct Answer: B**

**Explanation:**
**DynamoDB Global Tables** provide **active-active replication** across multiple regions with automatic conflict resolution.

---

### ✅ Exam Tip for SAA:

* **RDS** → Relational, managed, ACID
* **Aurora** → High performance + global scale
* **DynamoDB** → Serverless NoSQL, low latency
* **ElastiCache** → Caching, in-memory
* **Redshift** → Analytics & reporting

---
