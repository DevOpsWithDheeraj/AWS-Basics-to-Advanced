# AWS Snow Family

## 1. What is AWS Snow Family?

AWS Snow Family is a set of physical devices and services designed to **move large amounts of data between on-premises environments and AWS**. It helps in **data migration, edge computing, and disaster recovery** where network transfer is impractical due to bandwidth constraints or latency issues.  

The Snow Family includes:

- **AWS Snowcone**: Small, rugged, edge computing and data transfer device.
- **AWS Snowball Edge**: Larger storage and compute device for edge processing and migration.
- **AWS Snowmobile**: Extremely large-scale data transfer via a shipping truck for exabytes of data.

---

## 2. Features

- **Secure and Durable**: End-to-end encryption, tamper-resistant devices.
- **Edge Computing**: Snowcone and Snowball Edge can run compute workloads at the edge using AWS Lambda or EC2 instances.
- **Large Data Transfer**: Efficient migration of terabytes to exabytes of data.
- **Offline Operation**: Can work without continuous internet connectivity.
- **AWS Integration**: Seamlessly uploads data to S3, Glacier, or other AWS storage services.
- **Rugged and Portable**: Designed for harsh environments and physical transport.
- **Customizable Storage & Compute**: Snowball Edge allows running EC2 and Lambda workloads locally.

---

## 3. How to Configure AWS Snow Family

### Step 1: Choose the Device
- **Snowcone**: For small datasets (< 8 TB) and edge computing.
- **Snowball Edge Storage Optimized**: For large data transfer and storage-centric workloads.
- **Snowball Edge Compute Optimized**: For edge computing with higher compute capacity.
- **Snowmobile**: For extremely large migrations (up to 100 PB per truck).

### Step 2: Order Device from AWS Console
1. Go to **AWS Snow Family Console → Create Job**.
2. Select **Data Transfer or Edge Compute**.
3. Choose device type and size.
4. Provide shipping address for device delivery.

### Step 3: Set Up the Device
1. Once received, connect the device to your local network.
2. Unlock the device using the **Activation Code and Unlock Code** provided by AWS.
3. Mount storage volumes or configure NFS/SMB endpoints for data transfer.
4. For Snowball Edge, you can also launch **EC2 instances or Lambda functions** on the device.

### Step 4: Transfer Data
- Copy files locally to the device using CLI, SDK, or network shares.
- Verify data integrity using checksum validation.

### Step 5: Ship Device Back to AWS
- The device is returned via courier.
- AWS uploads the data to your specified S3 bucket or Glacier storage.

---

## 4. Use Cases

- **Data Migration**: Moving large datasets to AWS without relying on internet bandwidth.
- **Disaster Recovery**: Physical transport of backup data to AWS.
- **Edge Computing**: Processing data locally at remote sites with Snowball Edge or Snowcone.
- **Media & Entertainment**: Transferring massive video libraries to AWS.
- **Scientific Research**: Moving datasets from labs or observatories with limited network connectivity.

---

## 5. Pricing

- **Device Rental**: Charged per job (device usage), usually per day.
  - Snowcone: ~$0.03 per GB/day (storage + compute).
  - Snowball Edge: ~$300–500 per job for 10–14 days.
  - Snowmobile: Custom pricing per exabyte.
- **Data Transfer**:
  - Data upload via Snow Family devices is free when returned to AWS.
  - Outbound data transfer from AWS to on-premises is charged normally.
- **Additional Costs**:
  - Extended device usage beyond initial rental period.
  - Shipping costs for the device.

> Tip: AWS Snow Family is cost-effective for **large-scale data transfers** that would be impractical over internet links.

---

## 6. Best Practices

- Plan device usage: Estimate data size and choose appropriate device.
- Use checksum validation to ensure data integrity.
- Minimize on-device data processing to reduce job duration.
- Track device shipping and status in AWS Snow Family Console.
- Encrypt sensitive data with **KMS-managed keys**.
- Use edge compute capabilities for preprocessing large datasets before sending to AWS.
- Schedule jobs during non-critical operational periods to avoid disruption.

---

## 7. Practical Example: Migrating a Media Archive

### Scenario
A media company wants to move **500 TB of archived video content** from on-premises storage to AWS S3 for long-term storage and processing.

### Steps
1. Order **5 Snowball Edge Storage Optimized devices** from AWS Console.
2. Connect devices to local network upon arrival.
3. Unlock devices using provided codes.
4. Copy video files to the devices using AWS Snowball client or CLI.
5. Verify file integrity using checksums.
6. Ship devices back to AWS using pre-paid shipping labels.
7. AWS uploads all videos into the specified **S3 bucket**.
8. Enable **S3 Glacier lifecycle policy** for long-term cost optimization.

**Result:**  
The media archive is successfully migrated to AWS without saturating internet bandwidth, ensuring secure, durable, and cost-effective storage.

---

## 8. References
- [AWS Snow Family Documentation](https://docs.aws.amazon.com/snowball/latest/ug/whatissnow.html)
- [AWS Snow Family Pricing](https://aws.amazon.com/snowball/pricing/)
