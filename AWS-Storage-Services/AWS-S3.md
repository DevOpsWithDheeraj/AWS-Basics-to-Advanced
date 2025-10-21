# AWS S3 (Simple Storage Service)

## 1. What is AWS S3?
Amazon S3 (Simple Storage Service) is an object storage service offered by AWS that provides scalable, secure, and highly available storage for storing and retrieving any amount of data at any time. It is widely used for backup, data archiving, content storage, static website hosting, and big data analytics.

Key Features:
- **Durability:** 99.999999999% (11 nines) durability.
- **Scalability:** Automatically scales to store unlimited data.
- **Security:** Supports encryption (SSE-S3, SSE-KMS, SSE-C) and IAM policies.
- **Global Availability:** Data can be accessed from any AWS region.

---

## 2. How to Configure AWS S3

### Step 1: Create a Bucket
1. Log in to AWS Management Console.
2. Navigate to **S3 service**.
3. Click **Create bucket**.
4. Enter a **unique bucket name** and select the **region**.
5. Configure options such as versioning, encryption, and tags.
6. Set **bucket permissions** (public/private access).
7. Click **Create bucket**.

### Step 2: Upload Objects
1. Open the bucket.
2. Click **Upload** → **Add files/folders**.
3. Configure storage class, encryption, and metadata.
4. Click **Upload**.

### Step 3: Access Objects
- **Direct URL:** `https://<bucket-name>.s3.<region>.amazonaws.com/<object-key>`
- **Pre-signed URL:** Temporary access URL generated via AWS SDK or CLI.

### Step 4: Configure Lifecycle Policies (Optional)
- Set rules to transition objects to cheaper storage classes or delete old objects automatically.

---

## 3. Properties of an S3 Bucket
- **Versioning:** Maintain multiple versions of an object.
- **Encryption:** Server-side encryption (SSE-S3, SSE-KMS) or client-side encryption.
- **Logging:** Track access requests using server access logs.
- **Replication:** Cross-region replication (CRR) or same-region replication (SRR).
- **Tags:** Add metadata for cost allocation or categorization.
- **Object Lock:** Prevent accidental deletion for compliance.

---

## 4. Storage Classes & Pricing Model

| Storage Class                  | Use Case                                           | Pricing Model                  |
|--------------------------------|--------------------------------------------------|--------------------------------|
| **S3 Standard**                 | Frequently accessed data                         | Pay per GB stored + request charges |
| **S3 Intelligent-Tiering**      | Data with unknown access patterns                | Automatic tiering, pay per GB stored |
| **S3 Standard-IA (Infrequent Access)** | Infrequently accessed, but needs quick retrieval | Lower storage cost, retrieval fee applies |
| **S3 One Zone-IA**              | Infrequently accessed, single AZ storage        | Cheaper than Standard-IA, retrieval fee applies |
| **S3 Glacier**                  | Long-term archive, retrieval in minutes/hours   | Very low storage cost, retrieval cost applies |
| **S3 Glacier Deep Archive**     | Long-term archive, retrieval in 12 hours        | Lowest storage cost, retrieval cost applies |

**Pricing Model:**
- Charged for:
  - Storage used (per GB)
  - Requests (PUT, GET, COPY, LIST)
  - Data transfer out of AWS
  - Lifecycle transitions or retrieval (if using Glacier)

---

## 5. Permissions & Management

### Bucket & Object Permissions
- **Bucket Policies:** JSON-based policies for access control.
- **ACLs (Access Control Lists):** Grant read/write permissions to individual AWS accounts.
- **IAM Policies:** Control access for users and roles.
- **Public Access Settings:** Block public access globally or per bucket.

### Management Features
- **Lifecycle Policies:** Automate transitions/deletions.
- **Replication:** CRR and SRR.
- **Monitoring:** Use **CloudWatch**, **CloudTrail**, and **S3 Inventory**.
- **Event Notifications:** Trigger Lambda, SQS, or SNS on object events.

---

## 6. Best Practices
1. **Enable Versioning:** Prevent accidental deletions.
2. **Use Encryption:** Protect sensitive data (SSE-S3/SSE-KMS).
3. **Apply Lifecycle Policies:** Optimize cost by transitioning objects to cheaper storage classes.
4. **Enable MFA Delete:** Add extra layer of deletion protection.
5. **Use Proper Naming Conventions:** Easy identification and access.
6. **Monitor Usage:** Track access with CloudTrail and S3 analytics.
7. **Avoid Public Buckets:** Use presigned URLs for temporary access.
8. **Use Multipart Uploads:** Efficiently upload large files (>100 MB).

---

## 7. Practical Example: Hosting a Static Website

### Step 1: Create a Bucket
- Name the bucket same as your domain: `example.com`
- Enable **Public Access**.

### Step 2: Upload Website Files
- Upload `index.html`, `about.html`, `style.css`, `script.js`.

### Step 3: Enable Static Website Hosting
- Go to **Properties → Static Website Hosting**.
- Enter `index.html` as **Index Document**.
- Enter `error.html` as **Error Document** (optional).

### Step 4: Access Website
- Use the S3 website endpoint:  
  `http://example.com.s3-website-<region>.amazonaws.com`

### Step 5 (Optional): Configure Custom Domain
- Use **Route 53** to point your domain to the S3 website.

---

**Conclusion:**  
AWS S3 is a highly scalable, durable, and secure object storage service. It supports a variety of storage classes, fine-grained permissions, and management features, making it suitable for backups, archives, static websites, and big data workloads. By following best practices, you can optimize costs and security while using S3 effectively.
