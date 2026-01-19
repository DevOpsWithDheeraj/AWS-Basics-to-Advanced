
## 1️⃣ Object Storage for Web Assets

**Scenario:**
A company wants to store website images and videos that must be **highly durable**, **scalable**, and accessible over the internet. The company does not want to manage servers.

**Which AWS service should be used?**

A. Amazon EBS
B. Amazon EFS
C. Amazon S3
D. Amazon FSx

✅ **Correct Answer:** C. Amazon S3

**Explanation:**
Amazon S3 is **object storage** designed for massive scalability, **11 nines of durability**, and internet access. It is ideal for static website content, images, and videos.

---

## 2️⃣ Storage for EC2 Boot Volumes

**Scenario:**
An EC2 instance requires **persistent block storage** that remains available even after the instance is stopped or restarted.

**Which AWS storage service meets this requirement?**

A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. AWS Snowball

✅ **Correct Answer:** B. Amazon EBS

**Explanation:**
Amazon EBS provides **block-level storage** for EC2 and is commonly used for **OS and application data**. Data persists independently of the EC2 instance lifecycle.

---

## 3️⃣ Shared File System for Multiple EC2 Instances

**Scenario:**
A DevOps team needs a **shared file system** that can be accessed **simultaneously by multiple EC2 instances** across different Availability Zones.

**Which service should they choose?**

A. Amazon S3
B. Amazon EBS
C. Amazon EFS
D. Amazon FSx for Lustre

✅ **Correct Answer:** C. Amazon EFS

**Explanation:**
Amazon EFS is a **fully managed NFS file system** that supports **multiple EC2 instances concurrently** and scales automatically.

---

## 4️⃣ Low-Cost Long-Term Data Archival

**Scenario:**
A company must store compliance data for **10 years** that is **rarely accessed**, and cost is the top priority.

**Which S3 storage class is most suitable?**

A. S3 Standard
B. S3 Intelligent-Tiering
C. S3 Glacier Instant Retrieval
D. S3 Glacier Deep Archive

✅ **Correct Answer:** D. S3 Glacier Deep Archive

**Explanation:**
S3 Glacier Deep Archive is the **lowest-cost storage class**, designed for **long-term archival** where retrieval times can be hours.

---

## 5️⃣ Automatic Cost Optimization for Unknown Access Patterns

**Scenario:**
An application stores files in S3, but the access pattern is unpredictable. The company wants AWS to **automatically move data** to the most cost-effective tier.

**Which option should be used?**

A. S3 Standard
B. S3 Glacier
C. S3 Intelligent-Tiering
D. S3 One Zone-IA

✅ **Correct Answer:** C. S3 Intelligent-Tiering

**Explanation:**
S3 Intelligent-Tiering **automatically moves objects** between access tiers based on usage, optimizing costs without performance impact.

---

## 6️⃣ Temporary Storage for EC2

**Scenario:**
An application running on EC2 needs **very fast temporary storage** that will be deleted when the instance is stopped or terminated.

**Which storage option is best?**

A. Amazon EBS
B. Amazon EFS
C. Instance Store
D. Amazon S3

✅ **Correct Answer:** C. Instance Store

**Explanation:**
Instance Store provides **high-performance, temporary storage** physically attached to the host. Data is lost on stop/terminate.

---

## 7️⃣ On-Premises to AWS Large Data Transfer

**Scenario:**
A company needs to migrate **50 TB of on-premises data** to AWS but has limited internet bandwidth.

**Which AWS service should be used?**

A. AWS DataSync
B. AWS Snowball
C. Amazon S3 Transfer Acceleration
D. AWS Storage Gateway

✅ **Correct Answer:** B. AWS Snowball

**Explanation:**
AWS Snowball is a **physical data transfer device** used for large-scale migrations when network transfer is slow or impractical.

---

## 8️⃣ Hybrid Storage Access from On-Premises

**Scenario:**
An organization wants to access AWS storage from its on-premises environment while keeping existing applications unchanged.

**Which service enables this hybrid approach?**

A. Amazon EFS
B. AWS Snowball
C. AWS Storage Gateway
D. Amazon FSx

✅ **Correct Answer:** C. AWS Storage Gateway

**Explanation:**
AWS Storage Gateway connects **on-premises environments** with AWS cloud storage using standard file, volume, or tape interfaces.

---

## 9️⃣ High-Performance Windows File System

**Scenario:**
A company runs a **Windows-based application** that requires a fully managed **Windows file system** in AWS.

**Which service should be used?**

A. Amazon EFS
B. Amazon FSx for Windows File Server
C. Amazon S3
D. Amazon EBS

✅ **Correct Answer:** B. Amazon FSx for Windows File Server

**Explanation:**
FSx for Windows File Server provides **native Windows SMB support**, Active Directory integration, and high performance.

---

## 🔟 Multi-AZ Durable Object Storage

**Scenario:**
Which AWS storage service **automatically replicates data across multiple Availability Zones**?

A. Amazon EBS
B. Amazon EFS
C. Amazon S3
D. Instance Store

✅ **Correct Answer:** C. Amazon S3

**Explanation:**
Amazon S3 stores data **across multiple AZs by default**, providing high availability and durability.

---

### 📌 Exam Tip (Cloud Practitioner)

* **S3 → Object storage**
* **EBS → EC2 block storage**
* **EFS → Shared file system**
* **Glacier → Archival**
* **Snowball → Offline migration**
* **Storage Gateway → Hybrid storage**
