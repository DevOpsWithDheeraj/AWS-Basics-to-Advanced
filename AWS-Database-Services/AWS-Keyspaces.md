# 📘 Amazon Keyspaces (for Apache Cassandra) 

## 🔎 What is Amazon Keyspaces?

**Amazon Keyspaces** (for Apache Cassandra) is a fully managed, serverless database service that provides compatibility with the Apache Cassandra Query Language (CQL). It lets you run Cassandra workloads on AWS without provisioning, managing, or operating the underlying clusters. Keyspaces offers automatic scaling, high availability, encryption, and pay-for-use billing models, enabling developers to migrate or build Cassandra-style applications with minimal code changes.

---

## 🧩 Core Concepts

* **Keyspace**: A logical namespace similar to a database in relational systems. In Keyspaces, a keyspace defines replication strategy (SingleRegion or MultiRegion) but is a logical construct — the physical storage is fully managed by AWS.
* **Table**: Stores rows of data and is defined using CQL (CREATE TABLE). Tables support typical Cassandra data types and CQL constructs.
* **Partition key & Clustering columns**: Determine how data is partitioned and ordered. Proper schema design is critical for performance.
* **Consistency levels**: Keyspaces supports Cassandra consistency levels such as `LOCAL_QUORUM` and `LOCAL_ONE`. When using `cqlsh`, the client session must often set `CONSISTENCY LOCAL_QUORUM` before writes.
* **Capacity modes**: Two read/write capacity modes — **on-demand** (serverless, pay-per-request, auto-scales) and **provisioned** (reserve read/write capacity with autoscaling options).

---

## 🏗️ Architecture & Characteristics

* **Serverless managed service**: No nodes to provision or manage. AWS handles node management, replication, patching, and failover.
* **Replicated storage**: Data is replicated across multiple Availability Zones (AZs) in a region. Multi-Region keyspaces replicate data across regions for low-latency global reads and disaster recovery.
* **Cassandra-compatible API**: Supports CQL 3.11 APIs and many commonly used data-plane operations so most Cassandra drivers and client code work with Keyspaces with minimal changes.
* **Scaling**: On-demand capacity mode handles spiky traffic automatically. Provisioned mode allows you to reserve read/write capacity and configure autoscaling targets.
* **Durability & availability**: Built-in replication and fault tolerance provide high durability and availability without user-managed replicas.

---

## 🔁 Supported Features & Limitations

**Supported**

* CQL DDL/DML: `CREATE KEYSPACE`, `CREATE TABLE`, `INSERT`, `UPDATE`, `DELETE`, `SELECT`.
* Data types: Most common Cassandra types (text, int, bigint, boolean, timestamp, blob, list, map, set, uuid, etc.).
* Secondary indexes: Limited compared to self-managed Cassandra; use with care.
* Server-side features: Materialized views and some advanced cluster ops are not supported.

**Limitations**

* Keyspaces is not a drop-in replacement for every Cassandra feature. Some administrative or low-level tuning options available in self-managed Cassandra are not exposed.
* Some features (like certain UDT behaviors or full set of CQL functions) may have restrictions—check AWS docs for specifics.

---

## 🔒 Security & Compliance

* **Encryption at rest** by default (AWS KMS-managed keys or customer-managed keys).
* **Encryption in transit** using TLS for client connections.
* **VPC support & private connectivity** using AWS PrivateLink (interface VPC endpoints) for secure access from within your VPC.
* **IAM integration** for controlling who can manage Keyspaces resources; use IAM policies to limit API actions.
* **Fine-grained access** via resource-level permissions and integration with AWS CloudTrail for auditing.

---

## 💸 Pricing Model

* **On-demand mode**: Pay per request — reads (RRUs) and writes (WRUs) are metered. On-demand is ideal for unpredictable or spiky workloads.
* **Provisioned mode**: Reserve read and write capacity units, billed hourly. Suitable for predictable steady workloads and can be combined with autoscaling.
* **Storage & backup**: Storage is charged per GB-month and continuous backups or point-in-time recovery may have additional storage costs.

Costs vary by region — always consult the AWS Keyspaces pricing page and use Cost Explorer for table-level cost analysis.

---

## 🧰 Developer Experience & Tools

* **Drivers**: Cassandra drivers that support CQL 3.11 generally work (Java, Python, Node.js, .NET, etc.).
* **cqlsh**: Use the Cassandra shell for queries; remember to set consistency to `LOCAL_QUORUM` for write sessions when required.
* **AWS SDK & Console**: Create keyspaces and tables using the console, AWS SDKs, or CloudFormation.
* **Migration tools**: AWS Data Migration Service (DMS) and custom ETL scripts can help migrate from self-managed Cassandra clusters.

---

## 🧪 Practical Example — Building a Time-Series Events Table

### Scenario

You want to store sensor events from IoT devices. Each device produces time-stamped events and you need efficient writes and fast queries for recent events per device.

### Design Principles

* Use **device_id** as the partition key so events for a device are co-located.
* Use **event_time** as a clustering column (descending) so recent events are returned first.
* Use on-demand capacity mode for unpredictable traffic from many devices.

### Step 1 — Create a Keyspace

```sql
CREATE KEYSPACE iot_keyspace
WITH REPLICATION = {'class': 'SingleRegionStrategy'};
```

### Step 2 — Create Table

```sql
CREATE TABLE iot_keyspace.device_events (
  device_id text,
  event_time timestamp,
  event_id uuid,
  payload text,
  PRIMARY KEY (device_id, event_time, event_id)
) WITH CLUSTERING ORDER BY (event_time DESC);
```

### Step 3 — Insert Events

```sql
-- Ensure cqlsh session uses LOCAL_QUORUM for writes
CONSISTENCY LOCAL_QUORUM;

INSERT INTO iot_keyspace.device_events (device_id, event_time, event_id, payload)
VALUES ('device-123', toTimeStamp(now()), now(), '{"temp":28.5, "status":"ok"}');
```

### Step 4 — Query Recent Events for a Device

```sql
SELECT device_id, event_time, payload
FROM iot_keyspace.device_events
WHERE device_id = 'device-123'
LIMIT 20;
```

This schema provides high write throughput (writes are partitioned by device) and efficient queries for recent events per device.

---

## 🧭 Best Practices

* **Design your partition keys carefully**: Avoid hot partitions by ensuring partition keys have sufficient cardinality.
* **Use on-demand mode for spiky workloads**: It reduces the need for capacity planning.
* **Pre-warm new on-demand tables** when expecting a spike beyond default new-table limits.
* **Monitor metrics**: Use CloudWatch and table-level cost analytics to monitor read/write patterns and costs.
* **Use VPC endpoints and TLS** to secure client connections.
* **Test driver compatibility**: Validate your application with Keyspaces in a dev environment before production migration.

---

## 🧾 When to Use Amazon Keyspaces

Choose Keyspaces when you want Cassandra-like data model and CQL compatibility but prefer a fully managed, serverless experience on AWS. It’s especially useful for:

* IoT telemetry ingestion
* Time-series event stores
* User activity logs and analytics
* Large-scale, distributed workloads that benefit from a partitioned data model

---

## 🔗 References & Further Reading

* Amazon Keyspaces Developer Guide
* Amazon Keyspaces Pricing
* Working with CQL in Keyspaces
* Migrate Cassandra to Amazon Keyspaces

