
## **1. Amazon VPC Basics**

### **Question 1**

A company wants to launch AWS resources in a logically isolated virtual network where they can define IP ranges, subnets, and route tables. Which AWS service should they use?

A. Amazon Route 53
B. Amazon VPC
C. AWS Direct Connect
D. AWS Global Accelerator

✅ **Correct Answer:** **B. Amazon VPC**

**Explanation:**
Amazon VPC (Virtual Private Cloud) allows you to create a logically isolated network in AWS where you control IP address ranges, subnets, route tables, and gateways.

---

## **2. Public vs Private Subnet**

### **Question 2**

An EC2 instance must be accessible from the internet. Which configuration is REQUIRED?

A. Instance in a private subnet with a NAT Gateway
B. Instance in a public subnet with an Internet Gateway
C. Instance with only a private IP address
D. Instance in a VPC with no route table

✅ **Correct Answer:** **B. Instance in a public subnet with an Internet Gateway**

**Explanation:**
A public subnet has a route to an Internet Gateway (IGW). For internet access, the EC2 instance must be in a public subnet and have a public IP.

---

## **3. Internet Gateway (IGW)**

### **Question 3**

What is the primary purpose of an Internet Gateway in AWS?

A. Encrypt traffic within a VPC
B. Allow communication between VPCs
C. Enable internet access for VPC resources
D. Monitor network traffic

✅ **Correct Answer:** **C. Enable internet access for VPC resources**

**Explanation:**
An Internet Gateway enables communication between resources in a VPC and the internet.

---

## **4. NAT Gateway**

### **Question 4**

A company has EC2 instances in a private subnet that need outbound internet access for software updates. They must not be accessible from the internet. What should be used?

A. Internet Gateway
B. NAT Gateway
C. AWS Direct Connect
D. VPC Peering

✅ **Correct Answer:** **B. NAT Gateway**

**Explanation:**
A NAT Gateway allows instances in private subnets to initiate outbound internet connections while blocking inbound traffic.

---

## **5. Security Groups vs NACLs**

### **Question 5**

Which AWS networking feature acts as a **stateful firewall** at the instance level?

A. Network ACL
B. AWS Shield
C. Security Group
D. Route Table

✅ **Correct Answer:** **C. Security Group**

**Explanation:**
Security Groups are **stateful** and operate at the instance level. Network ACLs are stateless and work at the subnet level.

---

## **6. Network ACL Characteristics**

### **Question 6**

Which statement about Network ACLs (NACLs) is TRUE?

A. They are stateful
B. They apply to individual EC2 instances
C. They allow or deny traffic using numbered rules
D. They automatically allow return traffic

✅ **Correct Answer:** **C. They allow or deny traffic using numbered rules**

**Explanation:**
NACLs are stateless, apply at the subnet level, and evaluate rules in numerical order.

---

## **7. VPC Peering**

### **Question 7**

Two VPCs in the same AWS Region need private communication using private IP addresses. Which solution is MOST cost-effective?

A. AWS Transit Gateway
B. AWS Direct Connect
C. VPC Peering
D. Site-to-Site VPN

✅ **Correct Answer:** **C. VPC Peering**

**Explanation:**
VPC Peering allows private communication between two VPCs using AWS’s network without additional gateways.

---

## **8. AWS Transit Gateway**

### **Question 8**

A company wants to connect **multiple VPCs and on-premises networks** using a hub-and-spoke model. Which AWS service should be used?

A. VPC Peering
B. NAT Gateway
C. AWS Transit Gateway
D. Internet Gateway

✅ **Correct Answer:** **C. AWS Transit Gateway**

**Explanation:**
AWS Transit Gateway simplifies network architecture by acting as a central hub for connecting multiple VPCs and on-premises networks.

---

## **9. VPN Connectivity**

### **Question 9**

A company needs a **quick and secure** way to connect its on-premises data center to AWS over the internet. Which service should they choose?

A. AWS Direct Connect
B. Site-to-Site VPN
C. AWS Global Accelerator
D. VPC Peering

✅ **Correct Answer:** **B. Site-to-Site VPN**

**Explanation:**
Site-to-Site VPN uses IPsec tunnels over the public internet and is faster to set up compared to Direct Connect.

---

## **10. AWS Direct Connect**

### **Question 10**

Which AWS service provides **dedicated private network connectivity** between on-premises infrastructure and AWS?

A. Site-to-Site VPN
B. AWS Global Accelerator
C. AWS Direct Connect
D. Amazon CloudFront

✅ **Correct Answer:** **C. AWS Direct Connect**

**Explanation:**
AWS Direct Connect provides a dedicated, private, high-bandwidth connection that reduces latency and improves security.

---

## **11. Route 53**

### **Question 11**

A company wants to route users to the nearest AWS region based on latency. Which Amazon Route 53 routing policy should be used?

A. Simple routing
B. Weighted routing
C. Latency-based routing
D. Failover routing

✅ **Correct Answer:** **C. Latency-based routing**

**Explanation:**
Latency-based routing directs users to the region that provides the lowest latency.

---

## **12. VPC Endpoints**

### **Question 12**

An application in a private subnet must access Amazon S3 **without using the public internet**. What should be configured?

A. NAT Gateway
B. Internet Gateway
C. VPC Endpoint
D. VPC Peering

✅ **Correct Answer:** **C. VPC Endpoint**

**Explanation:**
VPC Endpoints allow private connectivity to AWS services like S3 without requiring internet access.

---

### 🔑 **Exam Tips for Networking (Cloud Practitioner)**

* Focus on **conceptual understanding**, not deep configurations
* Know differences between **IGW vs NAT**, **Security Group vs NACL**
* Understand **VPC Peering vs Transit Gateway**
* Route 53 routing policies are **frequently tested**

