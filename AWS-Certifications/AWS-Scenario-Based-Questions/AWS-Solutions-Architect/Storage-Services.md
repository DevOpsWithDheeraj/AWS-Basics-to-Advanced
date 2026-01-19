

## **1. Choosing Cost-Effective Storage for Infrequently Accessed Data**

A media company stores video files that are accessed only a few times per year but must be retrieved within minutes when needed. The company wants the **lowest storage cost** without long retrieval delays.

**Which AWS storage solution should be used?**

A. Amazon S3 Standard <br>
B. Amazon S3 Intelligent-Tiering <br>
C. Amazon S3 Glacier Flexible Retrieval <br>
D. Amazon S3 Glacier Deep Archive <br>

### ✅ **Correct Answer: C. Amazon S3 Glacier Flexible Retrieval**

**Explanation:**

* **S3 Glacier Flexible Retrieval** is designed for **rarely accessed data** with retrieval times ranging from **minutes to hours**.
* **Deep Archive** is cheaper but has **12+ hours** retrieval time.
* **S3 Standard** and **Intelligent-Tiering** cost more for infrequent access.

---

## **2. Storage for a High-Performance Database**

A company is running a mission-critical database on Amazon EC2 that requires **high IOPS, low latency, and consistent performance**.

**Which storage option should be used?**

A. Amazon EFS <br>
B. Amazon S3 <br>
C. Amazon EBS Provisioned IOPS (io2) <br>
D. Amazon S3 Glacier <br>

### ✅ **Correct Answer: C. Amazon EBS Provisioned IOPS (io2)**

**Explanation:**

* **EBS io2** provides **high, consistent IOPS** and is ideal for **databases**.
* **EFS** is for shared file systems, not high-performance databases.
* **S3** and **Glacier** are object storage, unsuitable for databases.

---

## **3. Shared File Storage Across Multiple EC2 Instances**

An application running on **multiple EC2 instances in different Availability Zones** needs a **shared file system** that automatically scales.

**Which AWS service should be used?**

A. Amazon EBS <br>
B. Amazon EFS <br>
C. Amazon S3 <br>
D. Amazon FSx for Windows File Server <br>

### ✅ **Correct Answer: B. Amazon EFS**

**Explanation:**

* **Amazon EFS** is a **managed NFS file system** that can be mounted by multiple EC2 instances across AZs.
* **EBS** can be attached to only one instance at a time.
* **S3** is object storage, not a file system.

---

## **4. Long-Term Compliance Data with No Immediate Access Needs**

A financial company must store audit logs for **10 years** for compliance. The data is rarely accessed and retrieval can take **several hours**.

**Which is the MOST cost-effective solution?**

A. Amazon S3 Standard <br>
B. Amazon S3 Glacier Instant Retrieval <br>
C. Amazon S3 Glacier Deep Archive <br>
D. Amazon EFS Infrequent Access <br>

### ✅ **Correct Answer: C. Amazon S3 Glacier Deep Archive**

**Explanation:**

* **Glacier Deep Archive** offers the **lowest cost** for long-term archival with retrieval times of **12–48 hours**.
* Ideal for compliance and regulatory data.

---

## **5. Storage for a Windows-Based Application**

A company is migrating a **Windows application** that requires **SMB protocol** and integration with **Active Directory**.

**Which AWS storage service should be used?**

A. Amazon EFS <br>
B. Amazon FSx for Windows File Server <br>
C. Amazon S3 <br>
D. Amazon EBS <br>

### ✅ **Correct Answer: B. Amazon FSx for Windows File Server**

**Explanation:**

* **FSx for Windows File Server** supports **SMB, NTFS, and Active Directory**.
* **EFS** uses NFS and is mainly for Linux workloads.

---

## **6. Automatically Optimizing Storage Costs**

A startup stores unpredictable data in Amazon S3. Some objects are frequently accessed, while others are rarely used. The company wants **automatic cost optimization** without performance impact.

**Which S3 storage class should be used?**

A. S3 Standard <br>
B. S3 One Zone-IA <br>
C. S3 Intelligent-Tiering <br>
D. S3 Glacier Instant Retrieval <br>

### ✅ **Correct Answer: C. S3 Intelligent-Tiering**

**Explanation:**

* **S3 Intelligent-Tiering** automatically moves objects between access tiers based on usage patterns.
* No retrieval fees and no performance impact.

---

## **7. Persistent Storage That Survives EC2 Termination**

An application running on EC2 requires **persistent block storage** that remains available even if the EC2 instance is stopped or terminated.

**Which storage service should be used?**

A. Instance Store <br>
B. Amazon EFS <br>
C. Amazon EBS <br>
D. Amazon S3 <br>

### ✅ **Correct Answer: C. Amazon EBS**

**Explanation:**

* **EBS volumes** persist independently of EC2 instance lifecycle.
* **Instance Store** data is lost when the instance stops or terminates.

---

## **8. High-Throughput File Storage for Machine Learning Workloads**

A data science team needs **high-throughput, low-latency file storage** for ML training workloads on Linux.

**Which service is BEST suited?**

A. Amazon EFS <br>
B. Amazon FSx for Lustre <br>
C. Amazon S3 <br>
D. Amazon Glacier <br>

### ✅ **Correct Answer: B. Amazon FSx for Lustre**

**Explanation:**

* **FSx for Lustre** is optimized for **high-performance computing (HPC) and ML workloads**.
* Integrates directly with Amazon S3 for data processing.

---

### 📌 **Exam Tips for SAA – Storage Services**

* **EBS = block storage** (databases, OS disks)
* **EFS = shared file storage (Linux)**
* **FSx = specialized file systems (Windows, Lustre)**
* **S3 = object storage** (scalability, durability)
* **Glacier = archival storage**
---
