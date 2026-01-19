
## 1️⃣ VPC Connectivity Between Regions

**Scenario:**
A company has applications running in **two different AWS Regions**. They need **private, encrypted connectivity** between the VPCs with **low latency** and **high bandwidth**. The solution should not use the public internet.

**Which solution should a Solutions Architect recommend?**

A. VPC Peering <br>
B. AWS VPN over the internet <br>
C. AWS Direct Connect <br>
D. Inter-Region VPC Peering <br>

✅ **Correct Answer: D. Inter-Region VPC Peering**

**Explanation:**

* **Inter-Region VPC Peering** allows private IP connectivity between VPCs in different regions.
* Traffic stays on the **AWS global network**, not the public internet.
* VPN uses the internet and has higher latency.
* Direct Connect is typically used for on-premises to AWS, not VPC-to-VPC.

---

## 2️⃣ Highly Available Internet-Facing Application

**Scenario:**
An application must be accessible globally and distribute traffic across multiple EC2 instances in different Availability Zones.

**Which AWS networking component ensures this?**

A. Network Load Balancer <br>
B. Application Load Balancer <br>
C. AWS Global Accelerator <br>
D. Amazon CloudFront <br>

✅ **Correct Answer: B. Application Load Balancer**

**Explanation:**

* **ALB** distributes HTTP/HTTPS traffic across multiple targets in multiple AZs.
* Supports path-based and host-based routing.
* CloudFront is a CDN, not a load balancer.
* Global Accelerator improves global performance but does not replace ALB routing logic.

---

## 3️⃣ Secure Access to S3 Without Internet

**Scenario:**
EC2 instances in a private subnet need to access **Amazon S3**, but the company wants to **avoid using NAT Gateway or Internet Gateway**.

**What is the most cost-effective solution?**

A. NAT Gateway <br>
B. Internet Gateway <br>
C. S3 Gateway Endpoint <br>
D. Interface Endpoint <br>

✅ **Correct Answer: C. S3 Gateway Endpoint**

**Explanation:**

* **Gateway Endpoints** allow private access to S3 and DynamoDB.
* No internet exposure and **no hourly charges**.
* NAT Gateway incurs hourly and data processing costs.
* Interface Endpoints are unnecessary for S3 in most cases.

---

## 4️⃣ Content Delivery with Low Latency

**Scenario:**
A media company serves video content to users worldwide. They want **low latency**, **high transfer speed**, and **reduced load on origin servers**.

**Which service should be used?**

A. Application Load Balancer <br>
B. AWS Global Accelerator <br>
C. Amazon CloudFront <br>
D. AWS Direct Connect <br>

✅ **Correct Answer: C. Amazon CloudFront**

**Explanation:**

* **CloudFront** is AWS’s CDN that caches content at **edge locations**.
* Reduces latency and offloads traffic from the origin.
* Global Accelerator improves TCP/UDP routing but does not cache content.

---

## 5️⃣ Hybrid Connectivity with Predictable Performance

**Scenario:**
A company wants a **dedicated, private connection** from its on-premises data center to AWS with **consistent network performance**.

**Which solution is best?**

A. Site-to-Site VPN <br>
B. Client VPN <br>
C. AWS Direct Connect <br>
D. VPC Peering <br>

✅ **Correct Answer: C. AWS Direct Connect**

**Explanation:**

* **Direct Connect** provides dedicated bandwidth and predictable latency.
* VPN uses the internet and may experience variable performance.
* VPC Peering does not connect on-premises networks.

---

## 6️⃣ Restrict Traffic at Subnet Level

**Scenario:**
A Solutions Architect needs to control inbound and outbound traffic **at the subnet level** and apply rules automatically.

**Which AWS service should be used?**

A. Security Groups <br>
B. Network ACLs <br>
C. AWS WAF <br>
D. Route Tables <br>

✅ **Correct Answer: B. Network ACLs**

**Explanation:**

* **Network ACLs** operate at the **subnet level**.
* They are **stateless**, meaning inbound and outbound rules must be defined.
* Security Groups are stateful and work at the instance level.

---

## 7️⃣ Improve Global Application Performance

**Scenario:**
A globally distributed application uses **TCP traffic** and requires **static IP addresses** and intelligent routing to the nearest AWS endpoint.

**Which service meets this requirement?**

A. Amazon CloudFront <br>
B. AWS Global Accelerator <br>
C. Application Load Balancer <br>
D. Route 53 Latency-Based Routing <br>

✅ **Correct Answer: B. AWS Global Accelerator**

**Explanation:**

* **Global Accelerator** provides **static anycast IPs** and routes traffic over AWS’s global network.
* Improves performance for non-HTTP traffic (TCP/UDP).
* CloudFront is for content caching (HTTP/HTTPS only).

---

## 8️⃣ DNS Failover Between Regions

**Scenario:**
An application is deployed in **two AWS Regions**. If one region fails, traffic must automatically route to the healthy region.

**Which Route 53 routing policy should be used?**

A. Weighted Routing <br>
B. Simple Routing <br>
C. Failover Routing <br>
D. Multivalue Answer Routing <br>

✅ **Correct Answer: C. Failover Routing**

**Explanation:**

* **Failover Routing** works with Route 53 health checks.
* Automatically redirects traffic when the primary endpoint becomes unhealthy.
* Weighted routing is for traffic distribution, not failure handling.

---

## 🔑 Exam Tips (Networking & CDN)

* **CloudFront = CDN + caching**
* **Global Accelerator = performance for TCP/UDP**
* **Gateway Endpoint = S3/DynamoDB only**
* **ALB = Layer 7, NLB = Layer 4**
* **NACL = Stateless, Security Group = Stateful**
* **Direct Connect = private + predictable**

---
