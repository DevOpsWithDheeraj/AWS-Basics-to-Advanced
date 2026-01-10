

1️⃣ DynamoDB Backup

🔹 What is a Backup in DynamoDB?

A backup is a full copy (snapshot) of a DynamoDB table at a specific point in time.

Once created, it never changes and is stored safely until you delete it.

🔹 Types of Backups

1. On-demand Backup (Manual)


2. AWS Backup–managed Backup (Policy-based)




---

🔹 Key Characteristics

Feature	Backup

Snapshot type	Full table snapshot
Data change after backup	❌ No (static copy)
Retention	Until deleted
Restore granularity	Only to backup creation time
Cost	Charged per backup size
Cross-region restore	✅ Yes



---

🔹 Example – DynamoDB Backup

Scenario: You have a table called Orders.

On 10 Jan 2026, 10:00 AM, you create an on-demand backup

At 12:00 PM, someone accidentally deletes data

You can restore the table exactly as it was at 10:00 AM


✅ Use case:

Before major deployment

Before schema change

Compliance & audits



---

🔹 How Restore Works

Restore creates a new table

Original table remains unchanged


📌 You cannot overwrite the existing table.


---

2️⃣ PITR (Point-in-Time Recovery)

🔹 What is PITR?

PITR continuously backs up your DynamoDB table and allows you to restore to any second within the last 35 days.

Think of it like a time machine ⏳.


---

🔹 Key Characteristics

Feature	PITR

Backup type	Continuous
Restore precision	Any second
Retention	Last 35 days
Manual effort	❌ None
Cost	Based on table size
Cross-region restore	❌ No



---

🔹 Example – DynamoDB PITR

Scenario: You have a table UserProfiles.

On 15 Jan, 10:00 AM → User data is correct

At 10:15 AM → A bug deletes thousands of items

At 10:30 AM → Issue detected


👉 Using PITR, you restore the table to 10:14:59 AM

✅ Exact second-level recovery


---

🔹 PITR Restore Behavior

Restore creates a new table

You choose:

Date

Time (to the second)




---

3️⃣ Backup vs PITR – Comparison Table

Feature	Backup	PITR

Creation	Manual / Policy	Automatic
Restore time	Backup timestamp only	Any second
Retention	Unlimited	35 days
Granularity	Coarse	Very fine
Operational effort	Manual	Minimal
Best for	Planned recovery	Accidental deletes



---

4️⃣ Real-World Use Case (Combined Approach)

🔹 E-commerce Application

PITR enabled → Protects from accidental deletes or bad deployments

On-demand backups → Taken before:

Schema updates

Application releases

Regulatory checkpoints



👉 Best practice: Use both together


---

5️⃣ Quick Interview Answer (Useful)

> Backup in DynamoDB is a full snapshot taken at a specific time, while PITR continuously backs up data and allows recovery to any second within the last 35 days. Backups are manual and static, whereas PITR is automatic and granular.




---
