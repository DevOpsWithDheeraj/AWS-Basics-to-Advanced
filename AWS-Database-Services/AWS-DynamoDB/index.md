

🔑 What is an Index in DynamoDB?

An index in DynamoDB is used to query data using attributes other than the table’s primary key.

👉 By default, DynamoDB allows queries only on:

Partition Key

Partition Key + Sort Key


If you want to query using any other attribute, you must create an Index.


---

🧱 Primary Index (Base Table)

Every DynamoDB table already has a Primary Index.

Types of Primary Key:

1. Partition Key only


2. Partition Key + Sort Key



Example:

Table: Orders
Partition Key: UserId
Sort Key: OrderId


---

📌 Types of Secondary Indexes in DynamoDB

DynamoDB supports two types of Secondary Indexes:

1. Local Secondary Index (LSI)


2. Global Secondary Index (GSI)




---

1️⃣ Local Secondary Index (LSI)

🔹 What is LSI?

A Local Secondary Index:

Uses the same Partition Key as the base table

Uses a different Sort Key


It is called Local because it works within the same partition.


---

🔹 Key Characteristics of LSI

Feature	LSI

Partition Key	Same as table
Sort Key	Different
Created	Only at table creation
Max per table	5
Read consistency	Strong & Eventual
Storage	Shared with table



---

🧪 LSI Example

🎯 Scenario: User Orders

Base Table: Orders

Attribute	Key

UserId	Partition Key
OrderId	Sort Key


Sample Data:

UserId	OrderId	OrderDate	Amount

U1	O101	2024-01-01	500
U1	O102	2024-01-10	300
U1	O103	2024-01-05	800



---

❓ Requirement

👉 Get all orders of a user sorted by OrderDate


---

🔹 Create LSI

LSI Name: OrderDateIndex
Partition Key: UserId
Sort Key: OrderDate


---

🔎 Query Example

UserId = 'U1'

✔ Same partition
✔ Different sort order
✔ Fast query


---

✅ When to Use LSI

Same Partition Key needed

Different sorting required

Strong consistency required



---

2️⃣ Global Secondary Index (GSI)

🔹 What is GSI?

A Global Secondary Index:

Can have a different Partition Key

Can have a different or no Sort Key


It is called Global because it can query data across all partitions.


---

🔹 Key Characteristics of GSI

Feature	GSI

Partition Key	Different
Sort Key	Optional
Created	Anytime
Max per table	20
Read consistency	Eventual only
Capacity	Separate RCU/WCU



---

🧪 GSI Example

🎯 Scenario

👉 Find all orders with status = SHIPPED


---

Base Table

PK: UserId
SK: OrderId


---

🔹 Create GSI

GSI Name: StatusIndex
Partition Key: OrderStatus
Sort Key: OrderDate


---

Sample Data:

UserId	OrderId	OrderStatus	OrderDate

U1	O101	SHIPPED	2024-01-01
U2	O201	SHIPPED	2024-01-02
U3	O301	PENDING	2024-01-03



---

🔎 Query Example

OrderStatus = 'SHIPPED'

✔ Across all users
✔ Different access pattern
✔ Highly scalable


---

✅ When to Use GSI

Query using non-key attributes

Cross-partition queries

Index creation after table creation



---

🔥 LSI vs GSI (Quick Comparison)

Feature	LSI	GSI

Partition Key	Same	Different
Sort Key	Different	Optional
Created At	Table creation	Anytime
Max Indexes	5	20
Strong Consistency	✅ Yes	❌ No
Capacity	Shared	Separate



---

🧠 Easy Memory Trick

LSI → Same PK, Local sorting

GSI → Different PK, Global access



---
