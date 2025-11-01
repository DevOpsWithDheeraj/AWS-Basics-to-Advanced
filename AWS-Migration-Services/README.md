# 🌐 AWS Migration Services

## 🧩 Overview

**AWS Migration Services** help organizations **move applications, data, and workloads** from on-premises environments, data centers, or other clouds to the **AWS Cloud** — securely, efficiently, and with minimal downtime.

AWS provides **tools, frameworks, and best practices** to simplify the **assessment, migration, and modernization** process.

---

## ⚙️ 1. Key AWS Migration Services

| Service                                              | Description                                                                                    | Use Case                                                 |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| **AWS Migration Hub**                                | Central tracking service for migration progress across multiple AWS and partner tools.         | Unified dashboard to track application migrations.       |
| **AWS Application Migration Service (MGN)**          | Automates **lift-and-shift (rehost)** migrations by replicating servers to AWS.                | Move on-premise servers (Windows/Linux) to EC2 easily.   |
| **AWS Database Migration Service (DMS)**             | Helps migrate **databases** to AWS quickly and securely with minimal downtime.                 | Migrate Oracle → Aurora, MySQL → RDS, etc.               |
| **AWS Server Migration Service (SMS)**               | Agentless service to migrate **virtual machines** (VMware, Hyper-V) to AWS.                    | Migrate large-scale VMs from data centers.               |
| **AWS Snow Family (Snowcone, Snowball, Snowmobile)** | Physical devices for **large-scale data transfer** when network bandwidth is limited.          | Transfer terabytes or petabytes of data to AWS.          |
| **AWS DataSync**                                     | Automates **online data transfer** between on-premise storage and AWS services like S3 or EFS. | Continuous or scheduled data synchronization.            |
| **AWS CloudEndure Migration**                        | Provides **disaster recovery** and migration solutions with real-time replication.             | Fast, reliable workload migration with minimal downtime. |

---

## 🧭 2. 6 R’s of Cloud Migration Strategy

AWS classifies migration strategies into **6 R’s**, which help determine the best approach for each workload.

| Strategy                                       | Description                                                                   | Example                                                    |
| ---------------------------------------------- | ----------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **1️⃣ Rehost (“Lift and Shift”)**              | Move applications **as-is** to AWS with little or no changes.                 | Migrate VMs from on-premise to EC2 using MGN.              |
| **2️⃣ Replatform (“Lift, Tinker, and Shift”)** | Make **minor optimizations** for better performance or cost before moving.    | Move app to EC2 but use RDS instead of self-managed DB.    |
| **3️⃣ Refactor / Re-architect**                | **Redesign** the application to take full advantage of cloud-native features. | Move monolithic app to microservices on AWS Lambda or ECS. |
| **4️⃣ Repurchase**                             | Replace the existing application with a **SaaS-based solution**.              | Replace CRM with Salesforce or ServiceNow.                 |
| **5️⃣ Retire**                                 | **Decommission** or remove applications that are no longer needed.            | Turn off legacy tools or duplicate systems.                |
| **6️⃣ Retain (Revisit / Re-evaluate)**         | Keep some workloads **on-premise** due to compliance or latency reasons.      | Keep mainframe workloads locally for now.                  |

---

## 🧱 3. 5 Phases of AWS Migration Process

AWS Migration journey generally follows **five key phases**, as defined in the **AWS Cloud Adoption Framework (CAF)**.

| Phase                                      | Description                                                               | Key Activities                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **1️⃣ Discovery & Assessment**             | Understand the current IT landscape and define migration goals.           | Inventory workloads, identify dependencies, and perform TCO analysis.     |
| **2️⃣ Mobilize**                           | Build the foundation for migration and address gaps found in assessment.  | Set up Landing Zone, security, governance, and pilot migrations.          |
| **3️⃣ Migration & Modernization**          | Move workloads to AWS using the right 6R strategy.                        | Execute migrations using MGN, DMS, or DataSync.                           |
| **4️⃣ Validation & Optimization**          | Verify migrated workloads and optimize for performance & cost.            | Conduct testing, performance tuning, and cost optimization.               |
| **5️⃣ Operation & Continuous Improvement** | Operate migrated applications efficiently with automation and monitoring. | Use CloudWatch, CloudTrail, and AWS Config for governance and monitoring. |

---

## 🧠 4. Example Scenario

**Company:** ABC Ltd. wants to migrate its on-premises web app to AWS.

1. **Assessment:** Identify current servers, dependencies, and costs.
2. **Mobilize:** Set up an AWS Landing Zone and security controls.
3. **Migration:** Use **AWS Application Migration Service** to rehost servers to EC2 and **DMS** for database migration.
4. **Validation:** Test performance, connectivity, and backups.
5. **Optimization:** Right-size EC2 instances and enable **Auto Scaling** and **CloudWatch** for monitoring.

---

## 🚀 5. Benefits of AWS Migration

* **Scalability:** Instantly scale resources based on demand.
* **Cost Efficiency:** Pay-as-you-go model.
* **Reliability:** Multi-AZ redundancy and automated backups.
* **Security:** Advanced compliance, IAM, and encryption.
* **Innovation:** Enables use of AI, ML, Serverless, and modern DevOps tools.

---

✅ **In Summary:**

| Concept                    | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| **AWS Migration Services** | Tools and services to move workloads and data to AWS.        |
| **6 R’s of Migration**     | Six strategies to choose the best migration approach.        |
| **5 Phases of Migration**  | Framework to plan and execute migration in a structured way. |

---
