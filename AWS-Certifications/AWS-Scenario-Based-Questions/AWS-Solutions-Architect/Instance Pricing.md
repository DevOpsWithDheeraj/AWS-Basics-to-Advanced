
## 1️⃣ Cost-Effective Compute for Steady Workloads

**Scenario:**
A company runs a web application on EC2 instances that operate **24/7 with predictable traffic**. The application will run for at least **3 years**. The company wants to **minimize EC2 costs**.

**Which pricing option should be used?**

A. On-Demand Instances <br>
B. Spot Instances <br>
C. Reserved Instances (3-year, All Upfront) <br>
D. EC2 Savings Plans (No Commitment) <br>

✅ **Correct Answer:** **C. Reserved Instances (3-year, All Upfront)**

**Explanation:**

* Reserved Instances provide **up to 72% cost savings** over On-Demand for long-term, steady usage
* Best for predictable workloads
* 3-year All Upfront gives **maximum discount**

---

## 2️⃣ Handling Unpredictable Traffic Spikes

**Scenario:**
An e-commerce website experiences **unpredictable spikes during sales events**. Instances must start quickly and may run only for a few hours.

**Which EC2 pricing model is MOST suitable?**

A. Reserved Instances <br>
B. Savings Plans <br>
C. On-Demand Instances <br>
D. Dedicated Hosts <br>

✅ **Correct Answer:** **C. On-Demand Instances**

**Explanation:**

* No long-term commitment
* Pay only for what you use
* Ideal for **short-term and unpredictable workloads**

---

## 3️⃣ Lowest Cost for Fault-Tolerant Batch Jobs

**Scenario:**
A media company processes large video files using batch jobs. Jobs can be **interrupted and restarted without issues**. Cost optimization is the top priority.

**Which pricing option should be used?**

A. On-Demand Instances <br>
B. Spot Instances <br>
C. Reserved Instances <br>
D. Dedicated Instances <br>

✅ **Correct Answer:** **B. Spot Instances**

**Explanation:**

* Spot Instances offer **up to 90% discount**
* Best for fault-tolerant, flexible workloads
* Can be interrupted with a 2-minute warning

---

## 4️⃣ Flexible Compute Usage Across Multiple Instance Types

**Scenario:**
A DevOps team runs multiple workloads across **different EC2 instance families** and regions. They want **maximum flexibility** with reduced costs.

**Which pricing model should they choose?**

A. Standard Reserved Instances <br>
B. Convertible Reserved Instances <br>
C. Compute Savings Plans <br>
D. EC2 Instance Savings Plans <br>

✅ **Correct Answer:** **C. Compute Savings Plans**

**Explanation:**

* Applies to **any EC2 instance family, region, OS, or tenancy**
* Up to **66% savings**
* More flexible than Reserved Instances

---

## 5️⃣ Licensing Requirements for Enterprise Software

**Scenario:**
A company runs a legacy application that requires a **bring-your-own license (BYOL)** model with **physical server visibility**.

**Which pricing option is REQUIRED?**

A. On-Demand Instances <br>
B. Reserved Instances <br>
C. Dedicated Hosts <br>
D. Spot Instances <br>
 
✅ **Correct Answer:** **C. Dedicated Hosts**

**Explanation:**

* Dedicated Hosts provide **full control over physical servers**
* Required for certain licensing and compliance needs
* More expensive but necessary for BYOL

---

## 6️⃣ Short-Term Testing Environment

**Scenario:**
Developers need EC2 instances for **testing new features**. Instances will be created and terminated multiple times per day.

**Which pricing option is MOST cost-effective?**

A. Spot Instances <br>
B. Reserved Instances <br>
C. On-Demand Instances <br>
D. Savings Plans <br>

✅ **Correct Answer:** **C. On-Demand Instances**

**Explanation:**

* No commitment
* Ideal for development and testing
* Charged per second (Linux) or per hour (Windows)

---

## 7️⃣ Switching Instance Families Over Time

**Scenario:**
A company wants long-term savings but expects to **change EC2 instance families** as their architecture evolves.

**Which pricing option should they choose?**

A. Standard Reserved Instances <br>
B. Convertible Reserved Instances <br>
C. Dedicated Instances <br>
D. Spot Instances <br>

✅ **Correct Answer:** **B. Convertible Reserved Instances**

**Explanation:**

* Allows **changing instance family, OS, or tenancy**
* Less discount than Standard RIs
* Good balance between savings and flexibility

---

## 8️⃣ Cost Optimization Without Instance Commitment

**Scenario:**
A startup wants cost savings on EC2 without committing to specific instance types or sizes.

**Which option meets this requirement?**

A. Standard Reserved Instances <br>
B. EC2 Instance Savings Plans <br>
C. Compute Savings Plans <br>
D. Dedicated Hosts <br>

✅ **Correct Answer:** **C. Compute Savings Plans**

**Explanation:**

* Commitment is based on **hourly spend**, not instance type
* Applies across services and regions
* Highly flexible and cost-effective

---

## 🔑 Exam Tips (Instance Pricing)

* **Predictable workload → Reserved Instances / Savings Plans**
* **Fault-tolerant → Spot Instances**
* **Short-term or unpredictable → On-Demand**
* **License or compliance needs → Dedicated Hosts**
* **Maximum flexibility → Compute Savings Plans**

---
