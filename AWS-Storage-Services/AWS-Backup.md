# AWS Backup

## 1. What is AWS Backup?

AWS Backup is a fully managed service that centralizes and automates **data backup across AWS services** and on-premises environments. It provides a **single console and API** to configure backup policies, monitor backup activity, and restore data reliably. AWS Backup supports services such as **EC2 EBS volumes, RDS databases, DynamoDB tables, EFS file systems, FSx file systems, and Storage Gateway volumes**.

AWS Backup helps organizations **meet regulatory compliance, recover from accidental deletions, and ensure business continuity**.

---

## 2. Features

- **Centralized Backup Management**: One place to manage backups for multiple AWS services.
- **Automated Backup Policies**: Define schedules, retention periods, and lifecycle rules.
- **Cross-Region and Cross-Account Backup**: Replicate backups across AWS regions and accounts for disaster recovery.
- **Compliance & Auditing**: Track backup activity for compliance reporting.
- **Cost Optimization**: Lifecycle policies automatically transition backups to lower-cost storage.
- **Restore Flexibility**: Restore to original or new resources, including point-in-time restores for databases.
- **Integration with Storage Gateway**: Backup on-premises data alongside cloud data.

---

## 3. How to Configure AWS Backup

### Step 1: Create a Backup Plan
1. Go to AWS Backup Console → **Create Backup Plan**.
2. Use **template** or **build your own plan**.
3. Configure:
   - **Backup frequency** (daily, weekly, monthly)
   - **Backup window**
   - **Lifecycle**: transition to cold storage (Glacier, Deep Archive)
   - **Retention period**

### Step 2: Assign Resources
- Select AWS resources (EC2 volumes, RDS instances, DynamoDB tables, EFS, FSx, Storage Gateway volumes).
- Tag resources to include in the backup plan.

### Step 3: Configure Backup Vault
- Create a **backup vault** to store backups securely.
- Enable **encryption** using AWS KMS.
- Set **access policies** for compliance.

### Step 4: Monitor & Restore
- Monitor backup activity via AWS Backup console or CloudWatch metrics.
- Restore resources to original or new location when needed.

---

## 4. Use Cases

- **Disaster Recovery**: Protect workloads across regions and accounts.
- **Compliance & Auditing**: Automate retention and reporting for regulatory requirements.
- **Data Protection**: Backup mission-critical databases, file systems, and block storage.
- **Hybrid Backup**: Protect on-premises data through Storage Gateway integration.
- **Application Resiliency**: Restore applications quickly with minimal downtime.

---

## 5. Pricing

- **Backup Storage**: Charged per GB per month for backup storage in AWS Backup.
  - Standard storage: Regular AWS storage pricing (EBS, S3, FSx, etc.).
  - Cold storage: Lower-cost storage in Glacier or Deep Archive.
- **Backup Requests**: Some AWS services charge per API request for backup.
- **Data Transfer**: Usually free within the same region; cross-region transfers incur charges.
- **Lifecycle Transitions**: Transition to cold storage reduces cost but adds retrieval latency.

> Tip: Use **lifecycle policies** to automatically move older backups to Glacier or Deep Archive for cost savings.

---

## 6. Best Practices

- Enable **cross-region backups** for disaster recovery.
- Encrypt backups using **AWS KMS**.
- Use **tags** to categorize resources for backup plans.
- Monitor backup activity and compliance with CloudWatch and AWS Config.
- Regularly test restores to ensure backup integrity.
- Optimize costs using **backup lifecycle policies**.
- Automate backup scheduling to reduce human error.

---

## 7. Practical Example: Backup EC2 EBS Volumes and RDS Databases

### Scenario
A company wants to protect its **EC2 instances and RDS databases** by creating automated daily backups with a 30-day retention period.

### Steps
1. Go to **AWS Backup Console → Create Backup Plan → Build a new plan**.
2. Configure backup plan:
   - Frequency: Daily at 2 AM
   - Retention: 30 days
   - Transition to cold storage after 15 days (optional)
3. Assign resources:
   - Select EC2 instances with associated EBS volumes.
   - Select RDS instances.
4. Create or select a **Backup Vault**:
   - Enable **KMS encryption**.
5. Monitor backups using the console:
   - Verify daily backup completion.
   - Test restore by creating a new EC2 instance from backup EBS snapshot.
6. Optional: Enable **cross-region replication** for DR.

**Result:**  
The company's EC2 and RDS resources are automatically backed up daily, securely stored, and recoverable with minimal effort, ensuring business continuity and compliance.

---

## 8. References
- [AWS Backup Documentation](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html)
- [AWS Backup Pricing](https://aws.amazon.com/backup/pricing/)
