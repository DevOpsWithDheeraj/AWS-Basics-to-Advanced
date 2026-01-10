

1️⃣ DynamoDB Export to S3

What is Export to S3?

Export to S3 allows you to export a DynamoDB table data to an Amazon S3 bucket without impacting table performance.

✔ No read capacity consumed
✔ Works on on-demand & provisioned tables
✔ Used mainly for backup, analytics, audit, ML, or migration


---

Types of Export

🔹 A) Export from PITR (Point-in-Time Recovery)

Export table data as it existed at any point in last 35 days

Requires PITR enabled

Most commonly used


🔹 B) Export from Current Table State

Export latest live data

No PITR required



---

Supported Formats

Format	Use case

DynamoDB JSON	Re-import to DynamoDB
ION	High-performance structured data
CSV	Athena, Redshift, Excel
Parquet	Analytics, Glue, Athena



---

Example: Export Orders Table to S3

Scenario
You have a DynamoDB table:

Table: Orders
Partition Key: OrderId
Sort Key: OrderDate

You want to export data for analytics using Athena.

Steps

1. Go to DynamoDB → Tables → Orders


2. Click Export to S3


3. Choose:

Export source: Current table state

Format: Parquet

S3 bucket: s3://company-dynamodb-backups/orders/



4. Start export



📦 Output stored in S3:

orders/
 ├── part-0001.parquet
 ├── part-0002.parquet

Now you can query it using Amazon Athena.


---

Common Use Cases

✅ Backup & disaster recovery
✅ Data lake creation
✅ Audit & compliance
✅ Machine learning training
✅ Cross-account or cross-region migration


---

2️⃣ DynamoDB Import from S3

What is Import from S3?

Import from S3 allows you to create a new DynamoDB table from data stored in S3.

⚠️ You cannot import into an existing table
✔ No write capacity used
✔ Fully serverless


---

Supported Input Formats

Format	Supported

DynamoDB JSON	✅
CSV	✅
ION	✅
Parquet	❌ (as of now)



---

Example: Import Orders Data from S3

Scenario
You exported a table earlier and now want to restore it in another region.

Steps

1. Go to DynamoDB → Import from S3


2. Select S3 location:

s3://company-dynamodb-backups/orders/


3. Choose format: DynamoDB JSON


4. Define new table:

Table name: Orders-Restore
Partition Key: OrderId
Sort Key: OrderDate


5. Start import



✔ New table created with all data


---

Import with CSV Example

CSV File in S3

OrderId,OrderDate,Customer,Amount
101,2024-01-10,Rahul,1200
102,2024-01-11,Amit,900

During import:

Map attributes

Define keys

DynamoDB automatically loads data



---

3️⃣ Export vs Import (Quick Comparison)

Feature	Export to S3	Import from S3

Direction	DynamoDB → S3	S3 → DynamoDB
Table required	Existing table	New table only
Affects capacity	❌ No	❌ No
Supported formats	JSON, CSV, ION, Parquet	JSON, CSV, ION
Restore use case	Backup	Recovery / Migration



---

4️⃣ Export/Import vs Backup/Restore

Feature	Export/Import	Backup/Restore

Table structure	Re-created	Preserved
Cross-account	✅ Yes	❌ No
Analytics ready	✅ Yes	❌ No
Speed	Slower	Faster
Cost	Cheaper for large data	Higher



---

5️⃣ Real-World Use Case (Interview-Ready)

Use Case: Multi-Region Data Migration

1. Export DynamoDB table from Mumbai region to S3


2. Copy S3 data to Ireland region


3. Import into new DynamoDB table


4. Enable Global Tables if required




---

6️⃣ Key Interview Points ⭐

Export does not consume RCU

Import does not consume WCU

Import creates new table only

Parquet is export-only

Best for large-scale migration & analytics

PITR enables historical exports



---

