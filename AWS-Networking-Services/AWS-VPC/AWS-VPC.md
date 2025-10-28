# 🌐 Amazon VPC (Virtual Private Cloud) 

## 📘 What is AWS VPC?

**Amazon Virtual Private Cloud (VPC)** is a **logically isolated virtual network** within the AWS Cloud where you can launch AWS resources in a controlled networking environment.  
VPC provides full control over:
- IP address ranges
- Subnets (public and private)
- Route tables
- Security configurations
- Gateways and network access

> Think of VPC as your **own private data center in the cloud**, fully configurable and secure.

---

## ⚙️ How to Configure a VPC

### Step-by-Step Configuration:

1. **Open the VPC Dashboard**
   - Navigate to **AWS Management Console → VPC → Create VPC**.

2. **Create a VPC**
   - Choose **VPC only**.
   - Assign **Name**: `MyVPC`.
   - CIDR block: `10.0.0.0/16` (65,536 IPs)
   - Tenancy: Default

3. **Create Subnets**
   - **Public Subnet**: `10.0.1.0/24` (for internet-facing resources)
   - **Private Subnet**: `10.0.2.0/24` (for internal resources)

4. **Attach an Internet Gateway**
   - Create IGW → `MyVPC-IGW`
   - Attach it to your VPC

5. **Create Route Tables**
   - **Public Route Table**: Add route `0.0.0.0/0 → IGW`
   - **Private Route Table**: Default or route via NAT Gateway

6. **Launch Instances**
   - EC2 instance in **public subnet** → assign public IP
   - EC2 instance or RDS in **private subnet** → no direct internet access

---

## 🧩 Components of a VPC

| Component | Description |
|------------|--------------|
| **VPC** | Logical network boundary; defines your IP range (CIDR block). |
| **CIDR Block** | IPv4/IPv6 range for VPC and subnets (e.g., 10.0.0.0/16). |
| **Subnet** | Subdivision of VPC; can be **public** or **private**. |
| **Public Subnet** | Subnet with route to Internet Gateway; hosts web-facing resources. |
| **Private Subnet** | Subnet without direct internet; internal resources like DBs. |
| **Route Table** | Controls how traffic is routed in the VPC/subnets. |
| **Security Group** | Instance-level virtual firewall (stateful). |
| **Network ACL (NACL)** | Subnet-level firewall (stateless). |
| **Internet Gateway (IGW)** | Allows communication between VPC and the Internet. |
| **NAT Gateway** | Allows private subnet resources to access Internet securely. |
| **VPC Endpoint** | Connects VPC privately to AWS services without internet. |
| **VPC Peering** | Enables private communication between two VPCs. |
| **Elastic IP** | Static IP address for internet-facing resources. |
| **DHCP Options Set** | Configures DNS and network options inside VPC. |
| **Flow Logs** | Logs all traffic for monitoring and auditing. |

---

## 🔐 Security Group vs Network ACL (NACL)

| Feature | Security Group | Network ACL |
|----------|----------------|-------------|
| Level | Instance | Subnet |
| Stateful | Yes | No |
| Rules | Allow only | Allow or Deny |
| Default Behavior | Deny inbound, allow outbound | Allow all inbound/outbound |
| Use Case | Control instance traffic | Control subnet traffic |

**Example:** Security group allows inbound SSH (22) to EC2; NACL blocks traffic from malicious IP ranges at subnet level.

---

## 🔗 VPC Endpoints

**VPC Endpoints** enable private connections to AWS services **without going through the Internet**.

### Types:

1. **Interface Endpoint (PrivateLink)**
   - Uses **ENI** in your subnet
   - Supports services like EC2, SNS, SQS, Lambda
   - Example: Private EC2 → DynamoDB

2. **Gateway Endpoint**
   - Only for **S3** and **DynamoDB**
   - Adds route in route table
   - Example: Access S3 privately without NAT Gateway

**Benefits:** Enhanced security, reduced latency, lower data transfer costs.

---

## 🌉 VPC Peering

**VPC Peering** connects two VPCs privately over AWS backbone.

- Works across same/different accounts or regions
- Traffic remains private
- No Internet Gateway or VPN required

**Use Cases:**
- Shared services between teams
- Multi-environment setups (Dev ↔ Prod)
- Centralized logging or monitoring

---

## 🌟 Use Cases of VPC

1. **Web Applications**
   - Public subnet for web servers, private for DBs
2. **Backend Services**
   - Databases, application servers isolated in private subnet
3. **Hybrid Cloud**
   - Connect on-premises networks via VPN or Direct Connect
4. **Multi-tier Architecture**
   - Presentation, application, and data layers separated
5. **Disaster Recovery**
   - Use multiple AZs for fault tolerance

---

## 🧱 Best Practices

1. Plan **CIDR blocks** to avoid overlap
2. Use multiple **Availability Zones**
3. Apply **least privilege** in security groups/NACLs
4. Separate **environments** (Dev, Test, Prod)
5. Enable **VPC Flow Logs**
6. Use **VPC Endpoints** for AWS services
7. Restrict **SSH access** to bastion hosts or VPN
8. Regularly review security rules

---

## 🧠 Practical Example: Deploying a 2-Tier App in VPC

**Scenario:** Host a web application with a public EC2 web server and private RDS database.

### Steps:

1. **Create VPC**
   - Name: `Prod-VPC`
   - CIDR: `10.0.0.0/16`

2. **Create Subnets**
   - Public: `10.0.1.0/24`
   - Private: `10.0.2.0/24`

3. **Internet Gateway**
   - Attach IGW to VPC
   - Public route table: `0.0.0.0/0 → IGW`

4. **NAT Gateway**
   - Place in Public subnet
   - Private route table: `0.0.0.0/0 → NAT Gateway`

5. **Security Groups**
   - Web-SG: Allow inbound HTTP/SSH
   - DB-SG: Allow inbound MySQL from Web-SG

6. **Launch Resources**
   - EC2 web server in public subnet
   - RDS DB in private subnet

7. **Test**
   - Access EC2 via browser
   - Web app connects to RDS securely internally

✅ Multi-tier, secure architecture complete.

---

## 🧾 Conclusion

Amazon VPC is the **foundation of AWS networking**, providing a **secure, scalable, and flexible network environment**.  
By understanding and configuring **subnets, gateways, route tables, security groups, NAT, endpoints, and peering**, you can design **production-ready, secure cloud architectures** that mimic enterprise-grade networks.

> **Key takeaway:** AWS VPC = **Your Private, Secure Cloud Network with Full Control**.

---

## ✅ Summary

| Topic | Description |
|--------|--------------|
| **Service** | Amazon Virtual Private Cloud (VPC) |
| **Purpose** | Isolated and secure virtual network for AWS resources |
| **Main Components** | Subnet, Route Table, IGW, NAT, NACL, Security Group |
| **Endpoints** | Interface & Gateway for private service access |
| **VPC Peering** | Connects VPCs privately across accounts or regions |
| **Security Controls** | Security Groups (Instance level), NACLs (Subnet level) |
| **Best Practices** | Multi-AZ setup, least privilege, enable Flow Logs |
| **Use Case Example** | Web + DB architecture with public/private subnets |
| **Conclusion** | Core of AWS networking, combining control, security, and scalability |

---
