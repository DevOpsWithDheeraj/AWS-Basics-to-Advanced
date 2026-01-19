

## 1. EC2 Security Patching Responsibility

A company runs a web application on Amazon EC2 instances using Amazon Linux. A recent vulnerability in the operating system kernel has been announced. Who is responsible for applying the security patch?

**A.** AWS <br>
**B.** The customer <br>
**C.** AWS Marketplace <br>
**D.** The EC2 Auto Scaling service <br>

✅ **Correct Answer: B. The customer**

**Explanation:**
Under the Shared Responsibility Model, AWS is responsible for **security of the cloud** (physical data centers, hardware, underlying infrastructure). Customers are responsible for **security in the cloud**, including:

* Guest operating system
* OS-level patches and updates
* Installed applications
  Since this is an OS kernel patch on EC2, it is the **customer’s responsibility**.

---

## 2. S3 Data Protection Responsibility

A startup stores sensitive customer documents in an Amazon S3 bucket. They want to ensure the data is encrypted at rest. Who is responsible for enabling and managing this encryption?

**A.** AWS automatically encrypts all data without customer involvement <br>
**B.** The customer <br>
**C.** AWS Support team <br>
**D.** Amazon S3 service team only <br>

✅ **Correct Answer: B. The customer**

**Explanation:**
AWS provides encryption capabilities (SSE-S3, SSE-KMS, SSE-C), but:

* **Choosing and enabling encryption**
* **Managing encryption keys (if using KMS or customer-managed keys)**
  are the **customer’s responsibilities**.

---

## 3. Physical Data Center Security

An enterprise asks who is responsible for securing AWS data centers against unauthorized physical access.

**A.** The customer’s security team <br>
**B.** The customer and AWS jointly <br>
**C.** AWS <br>
**D.** A third-party auditor <br>

✅ **Correct Answer: C. AWS**

**Explanation:**
AWS is responsible for:

* Physical security of data centers
* Surveillance, access control, guards
* Environmental protections
  This falls under **security of the cloud**, which is fully managed by AWS.

---

## 4. IAM Misconfiguration Incident

A developer accidentally assigns `AdministratorAccess` to an IAM user, leading to unauthorized resource deletion. Who is responsible for this security failure?

**A.** AWS <br>
**B.** The customer <br>
**C.** AWS IAM service <br>
**D.** Shared equally between AWS and customer <br>

✅ **Correct Answer: B. The customer**

**Explanation:**
IAM configuration, including:

* Users
* Roles
* Policies
* Permissions
  is the **customer’s responsibility**. AWS provides the IAM service, but **customers must configure it securely**.

---

## 5. Managed Database Patching

A company uses Amazon RDS for MySQL with automated backups enabled. Who is responsible for patching the underlying database engine?

**A.** The customer <br>
**B.** AWS <br>
**C.** The database vendor <br>
**D.** The customer’s DevOps team <br>

✅ **Correct Answer: B. AWS**

**Explanation:**
For **managed services** like Amazon RDS:

* AWS manages database engine patching
* AWS manages the underlying OS
  Customers remain responsible for:
* Database configuration
* Access control
* Data security

---

## 6. Network Security Groups Configuration

An application is hosted in a VPC with multiple EC2 instances. The application is exposed to the internet due to an overly permissive security group. Who is responsible?

**A.** AWS <br>
**B.** The customer <br>
**C.** Amazon VPC <br>
**D.** AWS Shield <br>

✅ **Correct Answer: B. The customer**

**Explanation:**
Customers are responsible for:

* Security group rules
* Network ACLs
* Firewall configurations
  AWS provides the networking tools, but **correct configuration is the customer’s duty**.

---

## 7. DDoS Protection at Infrastructure Level

A company experiences a large-scale DDoS attack targeting AWS infrastructure. Who protects the underlying infrastructure from such attacks?

**A.** The customer <br>
**B.** AWS <br>
**C.** Third-party security vendors <br>
**D.** Amazon EC2 Auto Scaling <br>

✅ **Correct Answer: B. AWS**

**Explanation:**
AWS protects:

* Global infrastructure
* Availability Zones
* Edge locations
  using built-in protections such as **AWS Shield Standard**. This is part of **security of the cloud**.

---

## 8. Lambda Function Vulnerability

A Lambda function contains vulnerable third-party libraries. Who is responsible for fixing this issue?

**A.** AWS <br>
**B.** The Lambda service <br>
**C.** The customer <br>
**D.** AWS Marketplace <br>

✅ **Correct Answer: C. The customer**

**Explanation:**
Even in **serverless services**:

* AWS manages the runtime, OS, and infrastructure
* Customers manage **application code and dependencies**
  Vulnerable libraries inside the function are the **customer’s responsibility**.

---

## 9. Data Classification Responsibility

A company must classify its data (public, confidential, regulated) before storing it in AWS services. Who is responsible for this task?

**A.** AWS <br>
**B.** The customer <br>
**C.** AWS Compliance team <br>
**D.** Amazon Macie <br>

✅ **Correct Answer: B. The customer**

**Explanation:**
AWS provides tools (like **Amazon Macie**) to help discover sensitive data, but:

* Data classification
* Data ownership
* Data handling policies
  are always the **customer’s responsibility**.

---

## 10. Hypervisor Security

A security team asks who is responsible for securing the hypervisor layer that runs EC2 instances.

**A.** The customer <br>
**B.** AWS <br>
**C.** EC2 instance owner <br>
**D.** IAM administrator <br>

✅ **Correct Answer: B. AWS**

**Explanation:**
The hypervisor is part of the **AWS infrastructure layer**, which includes:

* Compute hardware
* Virtualization layer
* Networking infrastructure
  This is fully managed by **AWS**.

---

### 📌 Exam Tip (Very Important for SAA)

* **EC2 → Customer manages OS & apps**
* **RDS/Lambda → AWS manages OS**
* **IAM, Security Groups, Data → Always customer**
* **Physical security & hypervisor → Always AWS**

---
