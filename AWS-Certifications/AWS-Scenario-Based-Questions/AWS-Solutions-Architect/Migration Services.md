
## 1. Large-Scale Data Center Migration

A company wants to migrate **300 on-premises servers** to AWS. They need to **track application dependencies** to avoid downtime during migration.

**Which AWS service should be used?**

A. AWS Migration Hub <br>
B. AWS Application Discovery Service <br>
C. AWS DataSync <br>
D. AWS Server Migration Service (SMS) <br>

✅ **Correct Answer: B**

**Explanation:**
AWS **Application Discovery Service** collects server utilization data and **maps dependencies** between applications, which is critical for planning large migrations. Migration Hub only tracks progress, not dependencies.

---

## 2. Tracking Migration Progress Across Tools

A solutions architect is migrating workloads using **AWS DMS, AWS SMS, and AWS DataSync**. Management wants a **single dashboard** to monitor migration status.

**Which service should be used?**

A. AWS CloudWatch <br>
B. AWS Migration Hub <br>
C. AWS Trusted Advisor <br>
D. AWS Systems Manager <br>

✅ **Correct Answer: B**

**Explanation:**
**AWS Migration Hub** provides a **centralized dashboard** to track migration progress across multiple AWS migration tools.

---

## 3. Minimal Downtime Database Migration

A MySQL database must be migrated to **Amazon Aurora MySQL** with **near-zero downtime**.

**Which service should be used?**

A. AWS Snowball <br>
B. AWS Database Migration Service (DMS) <br>
C. AWS DataSync <br>
D. AWS Backup <br>

✅ **Correct Answer: B**

**Explanation:**
AWS **DMS** supports **continuous data replication**, allowing source and target databases to stay in sync until cutover, minimizing downtime.

---

## 4. Migrating 100 TB Over Limited Bandwidth

A company needs to migrate **100 TB of on-premises data** to Amazon S3. Network bandwidth is limited and migration must complete quickly.

**Which solution is MOST cost-effective?**

A. AWS DataSync <br>
B. AWS Direct Connect <br>
C. AWS Snowball Edge <br>
D. AWS Storage Gateway <br>

✅ **Correct Answer: C**

**Explanation:**
**AWS Snowball Edge** is ideal for **large-scale offline data transfer**, eliminating bandwidth constraints and reducing transfer time.

---

## 5. Rehosting Virtual Machines Quickly

An organization wants to **lift and shift** VMware virtual machines to AWS with **minimal changes**.

**Which service should they use?**

A. AWS Application Migration Service (MGN) <br>
B. AWS Elastic Beanstalk <br>
C. AWS OpsWorks <br>
D. AWS DataSync <br>

✅ **Correct Answer: A**

**Explanation:**
**AWS Application Migration Service (MGN)** automates server replication and enables quick **rehosting (lift and shift)** to Amazon EC2.

---

## 6. Continuous File System Synchronization

A company wants to **continuously sync on-premises NFS data** to Amazon EFS during migration.

**Which service is BEST suited?**

A. AWS Snowcone <br>
B. AWS DataSync <br>
C. AWS Backup <br>
D. AWS Storage Gateway (Tape Gateway) <br>

✅ **Correct Answer: B**

**Explanation:**
**AWS DataSync** is designed for **online, incremental, and scheduled file transfers** between on-premises storage and AWS services.

---

## 7. Hybrid Access During Migration

An enterprise wants users to access **on-premises files** while data is being migrated to AWS.

**Which AWS service supports this requirement?**

A. AWS DataSync <br>
B. AWS Storage Gateway (File Gateway) <br>
C. AWS Snowball <br>
D. AWS Migration Hub <br>

✅ **Correct Answer: B**

**Explanation:**
**AWS Storage Gateway – File Gateway** provides **hybrid access**, allowing applications to access AWS-backed storage using standard file protocols.

---

## 8. Schema Conversion for Database Migration

A company is migrating an **Oracle database** to **Amazon Aurora PostgreSQL**.

**Which AWS tool helps convert database schemas?**

A. AWS DMS <br>
B. AWS SCT <br>
C. AWS Migration Hub <br>
D. AWS Glue <br>

✅ **Correct Answer: B**

**Explanation:**
**AWS Schema Conversion Tool (SCT)** converts database schemas, stored procedures, and code from one engine to another.

---

## 9. Assessing Readiness Before Migration

A company wants to **evaluate on-premises workloads** and receive migration recommendations.

**Which AWS service should be used?**

A. AWS Trusted Advisor <br>
B. AWS Migration Hub Strategy Recommendations <br>
C. AWS Application Migration Service <br>
D. AWS Compute Optimizer <br>

✅ **Correct Answer: B**

**Explanation:**
**Migration Hub Strategy Recommendations** analyzes workloads and provides **migration strategies** such as rehost, replatform, or refactor.

---

## 10. Ongoing Replication Until Cutover

A migration requires **ongoing replication** of EC2 workloads until the final switch to AWS.

**Which service supports this requirement?**

A. AWS Server Migration Service (SMS) <br>
B. AWS Application Migration Service (MGN) <br>
C. AWS DataSync <br>
D. AWS Snowball <br>

✅ **Correct Answer: B**

**Explanation:**
**AWS Application Migration Service (MGN)** supports **continuous block-level replication**, enabling seamless cutover with minimal downtime.

---

### 🎯 Exam Tip for SAA:

* **Discovery & Planning:** Application Discovery Service
* **Tracking:** Migration Hub
* **Databases:** DMS + SCT
* **Servers:** Application Migration Service (MGN)
* **Files:** DataSync / Storage Gateway
* **Large Offline Data:** Snowball

---
