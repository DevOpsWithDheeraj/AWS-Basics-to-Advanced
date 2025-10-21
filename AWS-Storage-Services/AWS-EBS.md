# AWS EBS (Elastic Block Store) 

## 1. What is AWS EBS?

Amazon Elastic Block Store (EBS) is a **high-performance block storage service** designed to be used with Amazon EC2 instances. Unlike object storage (S3), EBS provides **persistent, low-latency block storage** that behaves like a traditional hard drive and can be formatted, mounted, and used like a local disk.  

**Key Features:**
- **Persistent Storage:** Data persists even if the EC2 instance is stopped or terminated.
- **High Availability:** Data is replicated within an availability zone (AZ) to prevent failure.
- **Scalable:** Storage capacity can be increased dynamically without downtime.
- **Secure:** Supports encryption at rest and in transit.
- **Snapshot Support:** Create backups of volumes for disaster recovery or cloning.

**Use Cases:**
- Databases (MySQL, PostgreSQL, MongoDB)
- File systems (ext4, NTFS)
- Enterprise applications requiring persistent storage
- Big data workloads

---

## 2. How to Configure AWS EBS

### Step 1: Create an EBS Volume
1. Log in to the **AWS Management Console** → **EC2** → **Volumes** → **Create Volume**.
2. Choose:
   - **Volume Type** (e.g., gp3, io2)
   - **Size** (GB)
   - **IOPS** (for provisioned volumes)
   - **Availability Zone** (must match EC2 instance)
   - **Encryption** (optional)
3. Click **Create Volume**.

### Step 2: Attach Volume to EC2 Instance
1. Select the volume → **Actions → Attach Volume**.
2. Choose the **Instance ID** of the EC2 instance.
3. Click **Attach**.

### Step 3: Format and Mount (Linux Example)
```bash
# List block devices
lsblk

# Format volume (e.g., /dev/xvdf)
sudo mkfs -t ext4 /dev/xvdf

# Create mount point
sudo mkdir /mnt/mydata

# Mount volume
sudo mount /dev/xvdf /mnt/mydata

# Optional: Add to /etc/fstab for auto-mount
echo '/dev/xvdf /mnt/mydata ext4 defaults,nofail 0 2' | sudo tee -a /etc/fstab
````

---

## 3. Types of EBS Volumes

| Volume Type                                      | Use Case                                       | Performance Characteristics                                 |
| ------------------------------------------------ | ---------------------------------------------- | ----------------------------------------------------------- |
| **General Purpose SSD (gp3)**                    | Balanced price and performance                 | 3,000 IOPS baseline, up to 16,000 IOPS, low latency         |
| **Provisioned IOPS SSD (io2/io2 Block Express)** | Mission-critical databases requiring high IOPS | Up to 256,000 IOPS, 4,000 MB/s throughput                   |
| **Throughput Optimized HDD (st1)**               | Big data, data warehouses                      | Low cost, high throughput, not suitable for small I/O tasks |
| **Cold HDD (sc1)**                               | Infrequently accessed data                     | Lowest cost, low throughput, archival storage               |
| **Magnetic (standard)**                          | Legacy workloads                               | Low-cost, lower performance                                 |

---

## 4. Features of EBS

* **Snapshots:** Backup EBS volumes to S3 for durability.
* **Encryption:** Supports AES-256 encryption for data at rest and in transit.
* **Resize Volumes:** Dynamically increase size, IOPS, or type without downtime.
* **Multi-Attach:** Some io2 volumes can be attached to multiple EC2 instances simultaneously (for clustered apps).
* **High Availability:** Replicated within AZ to protect against hardware failure.
* **Tagging:** Add metadata for cost allocation and organization.

---

## 5. Pricing Model

EBS pricing depends on:

1. **Volume Type:** gp3, io2, st1, sc1, etc.
2. **Storage Size:** Price per GB per month.
3. **Provisioned IOPS:** For io2/io2 volumes, charged per IOPS.
4. **Snapshots:** Charged per GB stored in S3.
5. **Data Transfer:** Free within the same AZ; cross-AZ transfer may incur cost.

---

## 6. EBS vs Instance Store

| Feature              | EBS                                    | Instance Store                        |
| -------------------- | -------------------------------------- | ------------------------------------- |
| **Persistence**      | Persistent across instance stop        | Ephemeral; lost on instance stop      |
| **Storage Type**     | Network-attached block storage         | Physically attached to host           |
| **Performance**      | Slightly higher latency, consistent    | Extremely low latency, very high      |
| **Snapshots/Backup** | Supported via snapshots                | Not supported                         |
| **Attach/Detach**    | Can attach/detach between instances    | Cannot detach or move                 |
| **Use Case**         | Databases, file systems, critical data | Temporary data, caches, scratch space |

---

## 7. Best Practices

1. **Enable Snapshots:** Regularly back up critical volumes.
2. **Use gp3/Provisioned IOPS for DBs:** Ensure low-latency performance for transactional workloads.
3. **Encrypt Volumes:** Protect sensitive data using KMS.
4. **Use Multi-Attach for Clusters:** For high availability and shared access.
5. **Monitor Usage:** CloudWatch metrics for IOPS, throughput, and latency.
6. **Tag Volumes:** For cost allocation and better management.
7. **Separate OS and Data Volumes:** Avoid data loss during system updates.
8. **Avoid Over-Provisioning:** Optimize cost by right-sizing storage and IOPS.

---

## 8. Practical Example: Hosting a Database with EBS

### Step 1: Launch EC2 Instance

* Launch an EC2 instance (Linux) in `us-east-1` AZ.

### Step 2: Create EBS Volume

* Type: **gp3**
* Size: 100 GB
* IOPS: 3000 (optional)
* Availability Zone: Must match EC2 instance
* Encryption: Enabled

### Step 3: Attach EBS Volume

* Attach to EC2 instance as `/dev/xvdf`.

### Step 4: Format and Mount

```bash
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /mnt/dbdata
sudo mount /dev/xvdf /mnt/dbdata
```

### Step 5: Install Database (MySQL)

```bash
sudo yum install mysql-server -y
sudo systemctl start mysqld
sudo systemctl enable mysqld
# Move database data directory to EBS
sudo systemctl stop mysqld
sudo mv /var/lib/mysql /mnt/dbdata/mysql
sudo ln -s /mnt/dbdata/mysql /var/lib/mysql
sudo systemctl start mysqld
```

### Step 6: Take Snapshot (Optional)

* Create snapshot of the volume for backup:

```bash
aws ec2 create-snapshot --volume-id <volume-id> --description "Database backup"
```

---

## 9. Conclusion

AWS EBS provides **persistent, high-performance block storage** for EC2 instances. With multiple volume types, encryption, snapshots, and dynamic scaling, EBS is ideal for databases, applications, and enterprise workloads. Following best practices ensures durability, security, and cost-efficiency for your storage infrastructure.

---
