# AWS EFS (Elastic File System) 

## 1. What is AWS EFS?

Amazon Elastic File System (EFS) is a **fully managed, scalable, and elastic network file system** that can be used with AWS cloud services and on-premises resources. Unlike EBS, which provides block storage for a single EC2 instance, EFS provides **shared file storage** that multiple EC2 instances can access **concurrently**.  

**Key Characteristics:**
- **Fully Managed:** AWS handles maintenance, scaling, and reliability.
- **Elastic Scaling:** Automatically grows or shrinks as files are added or removed.
- **Concurrent Access:** Multiple instances can access the file system at the same time.
- **High Availability:** Stores data across multiple Availability Zones (AZs).
- **Secure:** Integrates with IAM, VPC, and supports encryption in transit and at rest.

**Use Cases:**
- Web serving and content management.
- Data sharing between EC2 instances.
- Containerized applications requiring shared storage.
- Big data and analytics workloads.
- Machine learning workflows.

---

## 2. How to Configure AWS EFS

### Step 1: Create an EFS File System
1. Log in to **AWS Management Console** → **EFS** → **Create file system**.
2. Configure:
   - **VPC:** Select the Virtual Private Cloud where EC2 instances reside.
   - **Availability Zones:** Choose multiple AZs for high availability.
   - **Performance Mode:**
     - **General Purpose:** Default, low-latency file operations.
     - **Max I/O:** Higher throughput for large-scale workloads.
   - **Throughput Mode:**
     - **Bursting:** Scales automatically.
     - **Provisioned:** Specify throughput in MB/s.
3. Enable **encryption** if required.
4. Click **Create File System**.

### Step 2: Configure Mount Targets
- Create **mount targets** in each AZ to allow EC2 instances to access EFS.
- Assign **security groups** to control access.

### Step 3: Mount EFS on EC2
```bash
# Install NFS client
sudo yum install -y nfs-utils      # Amazon Linux
sudo apt install -y nfs-common     # Ubuntu

# Create mount point
sudo mkdir /mnt/efs

# Mount EFS file system
sudo mount -t nfs4 -o nfsvers=4.1 <EFS-DNS-name>:/ /mnt/efs

# Optional: Add to /etc/fstab for auto-mount
echo '<EFS-DNS-name>:/ /mnt/efs nfs4 defaults,_netdev 0 0' | sudo tee -a /etc/fstab
````

---

## 3. Types of EFS

| Type                | Description                                                                 |
| ------------------- | --------------------------------------------------------------------------- |
| **General Purpose** | Default mode, low-latency file operations for most workloads.               |
| **Max I/O**         | High throughput for highly parallel workloads, e.g., big data or analytics. |

---

## 4. Storage Classes in EFS

EFS provides **two storage classes** to optimize cost:

| Storage Class              | Description                                                                                                      |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Standard**               | High availability and durability, used for frequently accessed files.                                            |
| **Infrequent Access (IA)** | Lower-cost storage for files accessed less frequently. Automatically transitions files based on access patterns. |

**Lifecycle Management:** You can automatically move files from Standard to IA after a set number of days to reduce costs.

---

## 5. Features of EFS

* **Elastic Scaling:** Automatically grows and shrinks with data.
* **Multi-AZ Availability:** Provides high availability and durability.
* **Shared Access:** Multiple EC2 instances, containers, and Lambda functions can access the file system.
* **Encryption:** Supports encryption at rest and in transit.
* **Access Control:** Integrates with IAM policies, VPC security groups, and POSIX permissions.
* **Backup & Restore:** Use AWS Backup for snapshots.
* **Performance Modes:** General Purpose or Max I/O.
* **Throughput Modes:** Bursting or Provisioned throughput.

---

## 6. Pricing Model

EFS pricing is based on:

1. **Storage Used:** Charged per GB per month (Standard or IA storage class).
2. **Provisioned Throughput (Optional):** Additional cost if provisioned throughput is used.
3. **Data Transfer:** Costs apply for data transfer across regions or out of AWS.
4. **Backup Costs:** Charged if using AWS Backup.

**Cost Optimization Tips:**

* Enable lifecycle management to move infrequently accessed files to IA.
* Use bursting throughput for general workloads.

---

## 7. Use Cases

1. **Shared File Storage:** For applications needing concurrent access from multiple EC2 instances.
2. **Content Management Systems:** WordPress, Drupal, or media hosting.
3. **Data Analytics & Big Data:** Shared storage for Hadoop, Spark, or EMR clusters.
4. **Containerized Workloads:** Shared volume for ECS or EKS pods.
5. **Machine Learning Workflows:** Store datasets accessible by multiple instances for training models.

---

## 8. Best Practices

1. **Use Multi-AZ Mount Targets:** Ensure high availability and low latency.
2. **Enable Lifecycle Management:** Move infrequently accessed files to IA to reduce costs.
3. **Use IAM Policies & Security Groups:** Restrict access to trusted instances and users.
4. **Monitor Performance:** Use CloudWatch metrics for throughput, IOPS, and latency.
5. **Backup Regularly:** Integrate with AWS Backup for snapshots.
6. **Choose Appropriate Performance Mode:** General Purpose for most apps, Max I/O for parallel workloads.
7. **Tag Resources:** For cost allocation and management.
8. **Avoid Over-Provisioned Throughput:** Start with bursting mode unless predictable throughput is required.

---

## 9. Practical Example: Shared Storage for Web Application

### Step 1: Create EFS File System

* VPC: `vpc-123456`
* AZs: `us-east-1a`, `us-east-1b`
* Performance Mode: General Purpose
* Throughput Mode: Bursting
* Encryption: Enabled

### Step 2: Create Mount Targets

* In each AZ, create mount targets for EC2 access.
* Assign security group allowing NFS (port 2049).

### Step 3: Launch EC2 Instances

* Launch two EC2 instances in the same VPC and AZs.

### Step 4: Mount EFS on Both Instances

```bash
sudo mkdir /mnt/efs
sudo mount -t nfs4 -o nfsvers=4.1 fs-12345678.efs.us-east-1.amazonaws.com:/ /mnt/efs
```

### Step 5: Deploy Application

* Both EC2 instances can read/write from `/mnt/efs`.
* Example: WordPress shared uploads folder stored in EFS for multiple web servers.

### Step 6 (Optional): Enable Lifecycle

* Automatically transition files older than 30 days to IA storage class.

---

## 10. Conclusion

AWS EFS is a **fully managed, scalable, and highly available network file system** ideal for applications requiring shared storage across multiple instances. With performance and throughput modes, lifecycle management, and multi-AZ support, EFS is perfect for web hosting, analytics, containerized applications, and machine learning workflows. Following best practices ensures cost efficiency, high availability, and secure data access.

---
