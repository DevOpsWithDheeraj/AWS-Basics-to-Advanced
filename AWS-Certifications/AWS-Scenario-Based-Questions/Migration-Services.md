
## **1. Choosing a Service for Large-Scale Database Migration**

A company wants to migrate its on-premises **Oracle database** to **Amazon Aurora** with **minimal downtime**. The database must remain available during the migration.

**Which AWS service should be used?**

A. AWS Snowball <br>
B. AWS Database Migration Service (AWS DMS) <br>
C. AWS DataSync <br>
D. AWS Storage Gateway <br>

✅ **Correct Answer:** **B. AWS Database Migration Service (AWS DMS)**

**Explanation:**
AWS DMS supports **continuous data replication**, allowing source databases to remain operational during migration. It is designed specifically for **low-downtime database migrations**.

---

## **2. Migrating Large Amounts of Data with Limited Network Bandwidth**

A media company needs to migrate **500 TB of data** from an on-premises data center to Amazon S3. The internet connection is slow and unreliable.

**Which AWS migration service is MOST appropriate?**

A. AWS DataSync <br>
B. AWS Snowmobile <br>
C. AWS Snowball Edge <br>
D. AWS DMS <br>

✅ **Correct Answer:** **C. AWS Snowball Edge**

**Explanation:**
AWS Snowball Edge is designed for **large-scale data transfers** when network bandwidth is limited. Snowmobile is used only for **exabyte-scale** data.

---

## **3. Migrating Multiple Servers to AWS with Minimal Refactoring**

A company wants to migrate **100 on-premises virtual machines** to AWS with **minimal application changes**.

**Which AWS service should they use?**

A. AWS Application Migration Service (MGN) <br>
B. AWS DMS <br>
C. AWS Migration Hub <br>
D. AWS Serverless Application Repository <br>

✅ **Correct Answer:** **A. AWS Application Migration Service (MGN)**

**Explanation:**
AWS Application Migration Service (formerly CloudEndure) enables **lift-and-shift server migrations** to AWS with minimal downtime and refactoring.

---

## **4. Tracking Migration Progress Across Multiple AWS Migration Tools**

An organization is using **AWS DMS, Snowball, and Application Migration Service**. Management wants a **central dashboard** to track migration progress.

**Which AWS service provides this capability?**

A. AWS CloudTrail <br>
B. AWS Migration Hub <br>
C. AWS Systems Manager <br>
D. AWS Organizations <br>

✅ **Correct Answer:** **B. AWS Migration Hub**

**Explanation:**
AWS Migration Hub provides a **single place to monitor and track migrations**, regardless of which AWS migration tools are used.

---

## **5. Continuous File System Migration to Amazon EFS**

A company wants to **continuously sync on-premises file data** to **Amazon EFS** with minimal manual effort.

**Which service should be used?**

A. AWS Storage Gateway <br>
B. AWS Snowball <br>
C. AWS DataSync <br>
D. AWS Transfer Family <br>

✅ **Correct Answer:** **C. AWS DataSync**

**Explanation:**
AWS DataSync is designed for **automated, continuous data transfer** between on-premises storage and AWS services like Amazon S3 and EFS.

---

## **6. Hybrid Storage Access During Migration**

A company wants on-premises applications to **access AWS storage as if it were local storage** during a migration phase.

**Which AWS service enables this hybrid approach?**

A. AWS DataSync <br>
B. AWS Snowball <br>
C. AWS Storage Gateway <br>
D. AWS Backup <br>

✅ **Correct Answer:** **C. AWS Storage Gateway**

**Explanation:**
AWS Storage Gateway provides **hybrid cloud storage**, allowing on-premises applications to access AWS storage seamlessly.

---

## **7. Database Migration Without Changing Database Engines**

A company wants to migrate a **MySQL database** from on-premises to Amazon RDS **without changing the database engine**.

**Which AWS service should be used?**

A. AWS Application Migration Service <br>
B. AWS DMS <br> 
C. AWS Snowball <br>
D. AWS Migration Hub <br>

✅ **Correct Answer:** **B. AWS DMS**

**Explanation:**
AWS DMS supports **homogeneous migrations** (same database engine) as well as heterogeneous migrations.

---

## **8. Assessing On-Premises Servers Before Migration**

A company wants to **collect server inventory and utilization data** to plan its migration to AWS.

**Which AWS service helps with this assessment?**

A. AWS Migration Hub <br>
B. AWS Application Discovery Service <br>
C. AWS Trusted Advisor <br>
D. AWS CloudWatch <br>

✅ **Correct Answer:** **B. AWS Application Discovery Service**

**Explanation:**
AWS Application Discovery Service gathers **server configuration and usage data** to help plan migrations.

---

### **Quick Exam Tip (Migration Services – CLF-C02)**

* **DMS** → Database migration with minimal downtime
* **Snowball / Snowmobile** → Offline data transfer
* **Application Migration Service** → Lift-and-shift servers
* **Migration Hub** → Migration tracking dashboard
* **DataSync** → Online file transfers
* **Storage Gateway** → Hybrid storage
---
