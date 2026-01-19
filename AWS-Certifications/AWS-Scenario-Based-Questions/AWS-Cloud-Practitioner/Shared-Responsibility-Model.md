

### **Question 1:**

A company is hosting a web application on **Amazon EC2** instances. They are responsible for patching the operating system and managing application-level security. AWS handles the physical infrastructure and hypervisor security. Which part of the shared responsibility model does this scenario illustrate?

**Options:**
A) AWS is responsible for all security, the customer has no responsibility. <br>
B) The customer is responsible for security “in the cloud,” AWS is responsible for security “of the cloud.” <br>
C) The customer is responsible for security “of the cloud,” AWS is responsible for security “in the cloud.” <br>
D) Both AWS and the customer share responsibility equally for patching the OS. <br>

**Answer:**
**B) The customer is responsible for security “in the cloud,” AWS is responsible for security “of the cloud.”**

**Explanation:**

* **AWS manages:** Physical infrastructure, network, storage, virtualization, and hypervisors (**security of the cloud**).
* **Customer manages:** Operating system, application patches, firewall configurations, and data (**security in the cloud**).
  This distinction is the core of the **AWS Shared Responsibility Model**.

---

### **Question 2:**

Your company wants to store sensitive customer data in **Amazon S3**. Who is responsible for encrypting the data at rest?

**Options:**
A) AWS automatically encrypts all data; the customer has no responsibility. <br>
B) AWS is responsible for the encryption keys. <br>
C) The customer is responsible for configuring encryption and key management if required. <br>
D) AWS and the customer both share responsibility for encryption automatically. <br>

**Answer:**
**C) The customer is responsible for configuring encryption and key management if required.**

**Explanation:**

* AWS provides encryption tools (S3 SSE-S3, SSE-KMS, SSE-C), but the **customer must choose whether to enable encryption** and manage keys if using customer-managed KMS keys.
* AWS ensures **physical and infrastructural security**, but **data-level encryption is the customer’s responsibility**.

---

### **Question 3:**

A company uses **AWS Lambda** for serverless functions. Who is responsible for applying OS patches?

**Options:**
A) Customer <br>
B) AWS <br>
C) Both AWS and the customer <br>
D) No one; Lambda does not require OS patches <br>

**Answer:**
**B) AWS**

**Explanation:**

* With **serverless services** like Lambda, **AWS manages the underlying infrastructure, OS, and runtime environment**.
* The customer only manages **function code, permissions, and environment configuration**.
* This demonstrates how responsibility shifts based on the **service model** (IaaS vs PaaS vs SaaS).

---

### **Question 4:**

Your organization is running a **database on Amazon RDS**. Who is responsible for **patching the database engine**?

**Options:**
A) AWS automatically handles all patches <br>
B) Customer must manually patch the database engine <br>
C) AWS handles infrastructure patches; customer may choose to enable automated database patching <br>
D) Customer handles everything <br>

**Answer:**
**C) AWS handles infrastructure patches; customer may choose to enable automated database patching**

**Explanation:**

* **AWS RDS** is a managed service. AWS manages **OS and database engine patching** if the customer enables **automatic patching**.
* Customer is responsible for **database configuration, users, access control, and data security**.

---

### **Question 5:**

A company is responsible for controlling access to AWS services and resources using **IAM policies**. Under the shared responsibility model, this responsibility falls under:

**Options:**
A) Security of the cloud <br>
B) Security in the cloud <br>
C) AWS responsibility <br>
D) AWS Shared services responsibility <br>

**Answer:**
**B) Security in the cloud**

**Explanation:**

* **IAM policies, user access, and permissions** are the customer’s responsibility.
* This is **security in the cloud**, meaning **AWS provides the tools**, but the **customer must configure and manage them correctly**.

---

✅ **Key Takeaways for Exam:**

1. **Security of the Cloud (AWS responsibility):** Physical security, hardware, networking, hypervisors, global infrastructure.
2. **Security in the Cloud (Customer responsibility):** Data, applications, OS, IAM, network configurations, encryption.
3. Responsibility **shifts with service type**: IaaS (EC2) → customer does more; PaaS (RDS, Lambda) → AWS does more.
4. Always remember: **“AWS manages the cloud, you manage in the cloud.”**

---
