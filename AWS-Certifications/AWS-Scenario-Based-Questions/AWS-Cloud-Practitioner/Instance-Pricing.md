

### **Question 1: On-Demand vs Reserved Instances**

**Scenario:**
A startup is running a web application and expects fluctuating traffic throughout the day. They need compute capacity immediately but are unsure about long-term usage.

Which AWS EC2 pricing model should they choose?

**Options:**
A. Spot Instances <br>
B. Reserved Instances (1-year or 3-year term) <br>
C. On-Demand Instances <br>
D. Dedicated Hosts <br>

**Answer:** C. On-Demand Instances

**Explanation:**

* **On-Demand Instances** allow you to pay for compute capacity **hourly or per second** without long-term commitments.
* Ideal for workloads with **unpredictable or fluctuating traffic**.
* **Reserved Instances** are better for predictable, long-term workloads.
* **Spot Instances** are cheap but can be interrupted, not suitable for critical apps.

---

### **Question 2: Cost Optimization with Spot Instances**

**Scenario:**
A company needs to run batch processing jobs that can tolerate interruptions. They want to **minimize compute costs**.

Which EC2 pricing model should they use?

**Options:**
A. On-Demand Instances <br>
B. Spot Instances <br>
C. Reserved Instances <br>
D. Dedicated Hosts <br>

**Answer:** B. Spot Instances

**Explanation:**

* **Spot Instances** allow you to bid for unused EC2 capacity at a **significant discount (up to 90%)**.
* They can be **terminated with 2 minutes’ notice**, so suitable only for **flexible or batch workloads**.
* On-Demand is more expensive, Reserved requires long-term commitment, Dedicated Hosts are not cost-efficient here.

---

### **Question 3: Predictable Workload**

**Scenario:**
A company runs a database server that needs to be **up 24/7** for the next 3 years. They want to **minimize cost** and have predictable usage.

Which EC2 pricing model is **most cost-effective**?

**Options:**
A. On-Demand Instances <br>
B. Reserved Instances (Standard) <br>
C. Spot Instances <br>
D. Dedicated Hosts <br>

**Answer:** B. Reserved Instances (Standard)

**Explanation:**

* **Reserved Instances** offer a **significant discount (up to 75%)** compared to On-Demand for long-term, predictable workloads.
* **Standard Reserved Instances** are ideal when instance type and region are known.
* Spot Instances are not reliable for 24/7 workloads.

---

### **Question 4: Flexible Workload with Savings Plans**

**Scenario:**
A company wants **flexibility** to change instance types across regions but also wants **cost savings** for steady workloads.

Which pricing option should they choose?

**Options:**
A. Standard Reserved Instances <br>
B. Convertible Reserved Instances <br>
C. Compute Savings Plans <br>
D. Dedicated Hosts <br>

**Answer:** C. Compute Savings Plans

**Explanation:**

* **Compute Savings Plans** allow you to **change instance family, size, OS, or region** while still receiving savings (up to 66%) for steady usage.
* **Convertible Reserved Instances** also allow flexibility but are less widely used than Savings Plans for compute flexibility.
* Dedicated Hosts are costlier and On-Demand doesn’t save much.

---

### **Question 5: Short-term Cost Savings**

**Scenario:**
A data analytics team runs experiments for only a few hours a day. They want **the cheapest option possible** without needing constant availability.

Which instance type should they use?

**Options:**
A. On-Demand Instances <br>
B. Spot Instances <br>
C. Standard Reserved Instances <br>
D. Dedicated Hosts <br>

**Answer:** B. Spot Instances

**Explanation:**

* Spot Instances are ideal for **short-lived or non-critical tasks** that can tolerate interruptions.
* They are much cheaper than On-Demand.
* On-Demand is flexible but **more expensive**, Reserved requires long-term commitment, Dedicated Hosts are unnecessary here.

---
