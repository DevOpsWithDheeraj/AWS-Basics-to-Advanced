
## **1. Amazon VPC Basics**

### **Question 1**

A company wants to launch AWS resources in a logically isolated virtual network where they can define IP ranges, subnets, and route tables. Which AWS service should they use?

A. Amazon Route 53 <br>
B. Amazon VPC <br>
C. AWS Direct Connect <br>
D. AWS Global Accelerator <br>

✅ **Correct Answer:** **B. Amazon VPC**

**Explanation:**
Amazon VPC (Virtual Private Cloud) allows you to create a logically isolated network in AWS where you control IP address ranges, subnets, route tables, and gateways.

---

## **2. Public vs Private Subnet**

### **Question 2**

An EC2 instance must be accessible from the internet. Which configuration is REQUIRED?

A. Instance in a private subnet with a NAT Gateway <br>
B. Instance in a public subnet with an Internet Gateway <br>
C. Instance with only a private IP address <br>
D. Instance in a VPC with no route table <br>

✅ **Correct Answer:** **B. Instance in a public subnet with an Internet Gateway**

**Explanation:**
A public subnet has a route to an Internet Gateway (IGW). For internet access, the EC2 instance must be in a public subnet and have a public IP.

---

## **3. Internet Gateway (IGW)**

### **Question 3**

What is the primary purpose of an Internet Gateway in AWS?

A. Encrypt traffic within a VPC <br>
B. Allow communication between VPCs <br>
C. Enable internet access for VPC resources <br>
D. Monitor network traffic <br>

✅ **Correct Answer:** **C. Enable internet access for VPC resources**

**Explanation:**
An Internet Gateway enables communication between resources in a VPC and the internet.

---

## **4. NAT Gateway**

### **Question 4**

A company has EC2 instances in a private subnet that need outbound internet access for software updates. They must not be accessible from the internet. What should be used?

A. Internet Gateway <br>
B. NAT Gateway <br>
C. AWS Direct Connect <br>
D. VPC Peering <br>

✅ **Correct Answer:** **B. NAT Gateway**

**Explanation:**
A NAT Gateway allows instances in private subnets to initiate outbound internet connections while blocking inbound traffic.

---

## **5. Security Groups vs NACLs**

### **Question 5**

Which AWS networking feature acts as a **stateful firewall** at the instance level?

A. Network ACL <br>
B. AWS Shield <br>
C. Security Group <br>
D. Route Table <br>

✅ **Correct Answer:** **C. Security Group**

**Explanation:**
Security Groups are **stateful** and operate at the instance level. Network ACLs are stateless and work at the subnet level.

---

## **6. Network ACL Characteristics**

### **Question 6**

Which statement about Network ACLs (NACLs) is TRUE?

A. They are stateful <br>
B. They apply to individual EC2 instances <br>
C. They allow or deny traffic using numbered rules <br>
D. They automatically allow return traffic <br>

✅ **Correct Answer:** **C. They allow or deny traffic using numbered rules**

**Explanation:**
NACLs are stateless, apply at the subnet level, and evaluate rules in numerical order.

---

## **7. VPC Peering**

### **Question 7**

Two VPCs in the same AWS Region need private communication using private IP addresses. Which solution is MOST cost-effective?

A. AWS Transit Gateway <br>
B. AWS Direct Connect <br>
C. VPC Peering <br>
D. Site-to-Site VPN <br>

✅ **Correct Answer:** **C. VPC Peering**

**Explanation:**
VPC Peering allows private communication between two VPCs using AWS’s network without additional gateways.

---

## **8. AWS Transit Gateway**

### **Question 8**

A company wants to connect **multiple VPCs and on-premises networks** using a hub-and-spoke model. Which AWS service should be used?

A. VPC Peering <br>
B. NAT Gateway <br>
C. AWS Transit Gateway <br>
D. Internet Gateway <br>

✅ **Correct Answer:** **C. AWS Transit Gateway**

**Explanation:**
AWS Transit Gateway simplifies network architecture by acting as a central hub for connecting multiple VPCs and on-premises networks.

---

## **9. VPN Connectivity**

### **Question 9**

A company needs a **quick and secure** way to connect its on-premises data center to AWS over the internet. Which service should they choose?

A. AWS Direct Connect <br>
B. Site-to-Site VPN <br>
C. AWS Global Accelerator <br>
D. VPC Peering <br>

✅ **Correct Answer:** **B. Site-to-Site VPN**

**Explanation:**
Site-to-Site VPN uses IPsec tunnels over the public internet and is faster to set up compared to Direct Connect.

---

## **10. AWS Direct Connect**

### **Question 10**

Which AWS service provides **dedicated private network connectivity** between on-premises infrastructure and AWS?

A. Site-to-Site VPN <br>
B. AWS Global Accelerator <br>
C. AWS Direct Connect <br>
D. Amazon CloudFront <br>

✅ **Correct Answer:** **C. AWS Direct Connect**

**Explanation:**
AWS Direct Connect provides a dedicated, private, high-bandwidth connection that reduces latency and improves security.

---

## **11. Route 53**

### **Question 11**

A company wants to route users to the nearest AWS region based on latency. Which Amazon Route 53 routing policy should be used?

A. Simple routing <br>
B. Weighted routing <br>
C. Latency-based routing <br>
D. Failover routing <br>

✅ **Correct Answer:** **C. Latency-based routing**

**Explanation:**
Latency-based routing directs users to the region that provides the lowest latency.

---

## **12. VPC Endpoints**

### **Question 12**

An application in a private subnet must access Amazon S3 **without using the public internet**. What should be configured?

A. NAT Gateway <br>
B. Internet Gateway <br>
C. VPC Endpoint <br>
D. VPC Peering <br>

✅ **Correct Answer:** **C. VPC Endpoint**

**Explanation:**
VPC Endpoints allow private connectivity to AWS services like S3 without requiring internet access.

---

### 🔑 **Exam Tips for Networking (Cloud Practitioner)**

* Focus on **conceptual understanding**, not deep configurations
* Know differences between **IGW vs NAT**, **Security Group vs NACL**
* Understand **VPC Peering vs Transit Gateway**
* Route 53 routing policies are **frequently tested**

