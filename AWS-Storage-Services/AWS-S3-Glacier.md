# AWS S3 Glacier & Glacier Deep Archive: 

## What is AWS S3 Glacier?

AWS S3 Glacier is a secure, durable, and low-cost cloud storage service designed for data archiving and long-term backup. It provides extremely low storage costs and is optimized for data that is **infrequently accessed** but must be retained for compliance, audits, or historical purposes.  

**Glacier Deep Archive** is the **lowest-cost storage class** in AWS S3, designed for **long-term retention of data** that is rarely accessed, such as regulatory archives or digital media preservation.

---

## Features

- **Durability & Reliability**: 99.999999999% (11 nines) durability.
- **Low-cost storage**: Ideal for infrequent access.
- **Flexible retrieval options**:
  - **Standard**: 3–5 hours
  - **Bulk**: 5–12 hours (Glacier)
  - **Expedited**: 1–5 minutes (Glacier)
  - Glacier Deep Archive: 12–48 hours
- **Data encryption**: Server-side encryption (SSE-S3 or SSE-KMS).
- **Lifecycle management**: Automatic transition from S3 Standard/IA to Glacier or Deep Archive.
- **Access control**: IAM policies, bucket policies, and S3 Access Points.
- **Compliance**: Supports WORM (Write Once Read Many) using S3 Object Lock.

---

## How to Configure AWS S3 Glacier

### Step 1: Create an S3 Bucket
1. Go to the AWS S3 Console → **Create Bucket**.
2. Name your bucket and select region.
3. Configure options like versioning, encryption, and tags.
4. Set bucket policies and access permissions.

### Step 2: Upload Data
- Directly upload files to the bucket.
- Alternatively, upload to **S3 Standard** and transition to Glacier using lifecycle rules.

### Step 3: Set Lifecycle Policies
- Go to **Management → Lifecycle rules** in your S3 bucket.
- Create a rule to transition objects:
  - **Glacier**: Move after X days from Standard/IA.
  - **Glacier Deep Archive**: Move after Y days.
- Set expiration if needed to delete old data automatically.

### Step 4: Retrieve Data
- Initiate retrieval via console, CLI, or SDK.
- Select retrieval type: Expedited, Standard, Bulk.
- Wait for completion depending on retrieval type.

---

## Use Cases

- Long-term backup for compliance or regulatory requirements.
- Archiving media files (videos, images) that are rarely accessed.
- Financial and healthcare records retention.
- Scientific and research datasets storage.
- Disaster recovery storage.

---

## Pricing

- **Storage Cost**:
  - Glacier: ~$0.004 per GB/month
  - Glacier Deep Archive: ~$0.00099 per GB/month
- **Retrieval Cost**:
  - Glacier Standard: $0.01 per GB
  - Glacier Expedited: $0.03 per GB
  - Glacier Bulk: $0.0025 per GB
  - Glacier Deep Archive: $0.02 per GB retrieval (bulk retrieval cheapest)
- **Additional Costs**:
  - PUT, GET, Lifecycle transitions, and data transfer out.
  
> Tip: Use **Glacier Deep Archive** for data that can tolerate **12–48 hour retrieval times**, and Glacier for data that may need faster access.

---

## Best Practices

- Use **lifecycle rules** to automatically move data to Glacier or Deep Archive.
- Enable **versioning** to protect against accidental deletions.
- Use **S3 Object Lock** for compliance or WORM requirements.
- Encrypt all data using SSE-S3 or SSE-KMS.
- Monitor storage and retrieval costs using AWS Cost Explorer.
- Minimize frequent retrievals to avoid high retrieval costs.

---

## Practical Example: Archiving Annual Financial Reports

### Scenario
Your company needs to retain financial reports for 7 years to meet regulatory compliance. Reports are rarely accessed, except during audits.

### Steps
1. Create an S3 bucket named `company-financial-archive`.
2. Enable **versioning** and **SSE-KMS encryption**.
3. Upload financial reports to the bucket.
4. Create a lifecycle rule:
   - Transition objects to **Glacier** after 30 days.
   - Transition to **Glacier Deep Archive** after 180 days.
5. Set an expiration of 7 years to delete old reports automatically.
6. For audit retrieval, initiate a **Standard retrieval** for the required files.

**Result:**  
Reports are safely archived at minimal cost, accessible when required, and automatically cleaned up after the retention period.

---

## References
- [AWS S3 Glacier Documentation](https://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html)
- [AWS S3 Pricing](https://aws.amazon.com/s3/pricing/)
- [AWS S3 Lifecycle Policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html)
