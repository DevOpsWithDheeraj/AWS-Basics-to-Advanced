
## 1. Choosing a Fully Managed Relational Database

**Scenario:**
A startup is building a web application that requires a **relational database**. The team does not want to manage backups, patching, or database software.

**Which AWS service should they use?**

A. Amazon EC2 with MySQL installed <br>
B. Amazon RDS <br>
C. Amazon DynamoDB <br>
D. Amazon S3 <br>

✅ **Correct Answer:** **B. Amazon RDS**

**Explanation:**
Amazon RDS is a **fully managed relational database service** that automates backups, patching, scaling, and maintenance. EC2 requires manual management, DynamoDB is NoSQL, and S3 is object storage.

---

## 2. High Availability for Relational Databases

**Scenario:**
A production database must remain available even if an **Availability Zone fails**.

**Which Amazon RDS feature provides this capability?**

A. Read Replicas <br>
B. Multi-AZ deployment <br>
C. Automated backups <br>
D. Manual snapshots <br>

✅ **Correct Answer:** **B. Multi-AZ deployment**

**Explanation:**
Multi-AZ deployments automatically replicate data to a standby instance in another AZ and provide **automatic failover**, ensuring high availability.

---

## 3. Choosing a Serverless NoSQL Database

**Scenario:**
A mobile application experiences **unpredictable traffic spikes** and requires **single-digit millisecond latency** with no server management.

**Which AWS service is best?**

A. Amazon Aurora <br>
B. Amazon RDS <br>
C. Amazon DynamoDB <br>
D. Amazon Redshift <br>

✅ **Correct Answer:** **C. Amazon DynamoDB**

**Explanation:**
DynamoDB is a **serverless NoSQL key-value database** that automatically scales and delivers low-latency performance.

---

## 4. Database for Analytics and Reporting

**Scenario:**
A company wants to analyze **terabytes of historical data** for business intelligence and reporting.

**Which AWS service is most appropriate?**

A. Amazon RDS <br>
B. Amazon DynamoDB <br>
C. Amazon Aurora <br>
D. Amazon Redshift <br>

✅ **Correct Answer:** **D. Amazon Redshift**

**Explanation:**
Amazon Redshift is a **data warehouse** optimized for analytical queries and large-scale reporting workloads.

---

## 5. Improving Read Performance for RDS

**Scenario:**
An application reads data frequently from an Amazon RDS database. The database performance is slow during peak hours.

**Which solution improves read performance?**

A. Enable Multi-AZ <br>
B. Add Read Replicas <br>
C. Increase backup retention <br>
D. Take manual snapshots <br>

✅ **Correct Answer:** **B. Add Read Replicas**

**Explanation:**
Read Replicas offload read traffic from the primary database, improving performance for read-heavy workloads.

---

## 6. Fully Managed MySQL-Compatible Database with High Performance

**Scenario:**
A company needs a **MySQL-compatible database** with **higher performance and availability** than standard RDS.

**Which service should be used?**

A. Amazon DynamoDB <br>
B. Amazon Aurora <br>
C. Amazon Redshift <br>
D. Amazon ElastiCache <br>

✅ **Correct Answer:** **B. Amazon Aurora**

**Explanation:**
Amazon Aurora is a **high-performance, MySQL/PostgreSQL-compatible** relational database offering better scalability and availability than standard RDS engines.

---

## 7. In-Memory Database for Caching

**Scenario:**
An application needs **microsecond-level latency** for frequently accessed data such as session information.

**Which AWS service is best?**

A. Amazon RDS <br>
B. Amazon DynamoDB <br>
C. Amazon ElastiCache <br>
D. Amazon Redshift <br>

✅ **Correct Answer:** **C. Amazon ElastiCache**

**Explanation:**
ElastiCache (Redis or Memcached) is an **in-memory data store** ideal for caching and real-time data access.

---

## 8. Automatic Scaling for DynamoDB

**Scenario:**
A DynamoDB table experiences unpredictable workload changes.

**Which feature helps manage capacity automatically?**

A. Global Tables <br>
B. DynamoDB Streams <br>
C. On-Demand Capacity Mode <br>
D. Encryption at rest <br>

✅ **Correct Answer:** **C. On-Demand Capacity Mode**

**Explanation:**
On-Demand mode automatically scales read/write capacity based on traffic without capacity planning.

---

## 9. Disaster Recovery for Databases

**Scenario:**
A company wants to protect its database from accidental deletion.

**Which feature helps restore data to a previous point in time?**

A. Read Replicas <br>
B. Multi-AZ <br>
C. Point-in-Time Recovery <br>
D. Global Tables <br>

✅ **Correct Answer:** **C. Point-in-Time Recovery**

**Explanation:**
Point-in-Time Recovery (PITR) allows restoring a database to any second within the retention period.

---

## 10. Globally Distributed NoSQL Database

**Scenario:**
A globally distributed application requires **low-latency access** for users in multiple regions.

**Which AWS service should be used?**

A. Amazon RDS Multi-AZ <br>
B. Amazon Aurora <br>
C. Amazon DynamoDB Global Tables <br>
D. Amazon Redshift <br>

✅ **Correct Answer:** **C. Amazon DynamoDB Global Tables**

**Explanation:**
DynamoDB Global Tables provide **multi-region replication**, enabling low-latency access for global users.

---

### 📌 Exam Tip (Cloud Practitioner)

* **RDS & Aurora** → Relational workloads
* **DynamoDB** → Serverless NoSQL, low latency
* **Redshift** → Analytics & reporting
* **ElastiCache** → In-memory caching
