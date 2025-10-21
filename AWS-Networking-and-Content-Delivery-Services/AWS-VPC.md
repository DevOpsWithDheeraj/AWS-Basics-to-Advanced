# 🌐 Amazon VPC (Virtual Private Cloud) 

## 📘 What is AWS VPC?

**Amazon Virtual Private Cloud (VPC)** is a **logically isolated section of the AWS Cloud** where you can launch and manage AWS resources (like EC2, RDS, etc.) in a **customized virtual network** that you define.

VPC gives you **full control over your networking environment**, including:
- IP address ranges
- Subnets
- Route tables
- Internet gateways
- Security settings

In simple words:  
> AWS VPC is your **own private data center** inside AWS, with total control over networking and security.

---

## ⚙️ How to Configure a VPC

### 🪜 Step-by-Step VPC Configuration

1. **Open the VPC Dashboard**
   - Go to **AWS Management Console → VPC → Create VPC**.

2. **Create a VPC**
   - Choose **VPC only**.
   - Assign **Name tag**: `MyVPC`.
   - CIDR block: `10.0.0.0/16` (gives 65,536 IPs).
   - Select **Tenancy**: Default.

3. **Create Subnets**
   - Public Subnet: `10.0.1.0/24` (for internet-facing resources)
   - Private Subnet: `10.0.2.0/24` (for internal resources)

4. **Create and Attach an Internet Gateway**
   - Create an **Internet Gateway (IGW)** → `MyVPC-IGW`.
   - Attach it to your VPC.

5. **Create Route Tables**
   - Public Route Table: Add route `0.0.0.0/0 → IGW`.
   - Private Route Table: Default (no direct internet access).

6. **Launch an EC2 Instance**
   - Choose **Public Subnet** and **enable Auto-assign Public IP**.
   - Attach a **Security Group** allowing SSH (port 22) and HTTP (port 80).

✅ You now have a working VPC with both public and private networks.

---

## 🧩 Components of a VPC

| Component | Description |
|------------|--------------|
| **VPC** | Virtual network that defines your IP range (CIDR block). |
| **Subnet** | A smaller network segment within a VPC (Public or Private). |
| **Route Table** | Defines how traffic is directed within the VPC. |
| **Internet Gateway (IGW)** | Allows communication between VPC and the internet. |
| **NAT Gateway** | Allows private instances to access the internet securely. |
| **Security Group** | Virtual firewall controlling **inbound/outbound** traffic for instances. |
| **Network ACL (NACL)** | Firewall controlling traffic at the **subnet level**. |
| **VPC Endpoint** | Connects VPC privately to AWS services without internet. |
| **VPC Peering** | Connects two VPCs to communicate privately using AWS backbone. |
| **Elastic IP** | Static IP address for internet-facing resources. |
| **DHCP Options Set** | Controls domain name resolution within the VPC. |
| **Flow Logs** | Captures network traffic logs for analysis and troubleshooting. |

---

## 🌟 Key Features and Properties

1. **Complete Network Control**
   - Define your IP address range, subnets, routing, and access.
2. **Security**
   - Use Security Groups and NACLs for multi-layered protection.
3. **Scalability**
   - Easily add subnets, route tables, or gateways.
4. **Hybrid Connectivity**
   - Connect on-premises networks via VPN or AWS Direct Connect.
5. **High Availability**
   - Create subnets across multiple **Availability Zones (AZs)**.
6. **Monitoring**
   - Enable **VPC Flow Logs** to capture network activity.

---

## 🔐 Security Group vs Network ACL (NACL)

| Feature | Security Group | Network ACL |
|----------|----------------|-------------|
| **Level** | Instance level | Subnet level |
| **Stateful/Stateless** | Stateful | Stateless |
| **Rules** | Allow only | Allow or Deny |
| **Default Behavior** | Deny all inbound, allow all outbound | Allow all inbound/outbound |
| **Use Case** | Control traffic for specific EC2 instances | Control traffic for entire subnet |

### Example:
- Use **Security Group** to allow inbound SSH (22) to a web server.
- Use **NACL** to block malicious IP ranges at the subnet level.

---

## 🔗 VPC Endpoints

**VPC Endpoints** enable private connections between your VPC and supported AWS services **without using the public Internet**.

### Types of Endpoints

1. **Interface Endpoint (PrivateLink)**
   - Uses **Elastic Network Interface (ENI)**.
   - Supports services like S3, DynamoDB, SNS, SQS.
   - Example: Connect EC2 → S3 privately.

2. **Gateway Endpoint**
   - Works with **S3** and **DynamoDB** only.
   - Creates a route in the Route Table.
   - Example: Access S3 privately without NAT Gateway.

### Benefits:
- Improved security (no internet exposure)
- Reduced latency
- Lower data transfer costs

---

## 🌉 VPC Peering

**VPC Peering** allows two VPCs to communicate privately over the **AWS backbone network**.

- Works across the **same or different AWS accounts** and **regions**.
- No single point of failure.
- Traffic remains private — no need for an Internet Gateway or VPN.

### Use Cases:
- Shared services between teams.
- Multi-environment architecture (Dev ↔ Prod communication).
- Centralized logging or monitoring VPC.

### Example:
Connect VPC A (10.0.0.0/16) with VPC B (192.168.0.0/16) for internal application communication.

---

## 💡 Use Cases of VPC

1. **Host Web Applications**
   - Public subnets for web servers, private subnets for databases.
2. **Secure Backend Services**
   - Databases and application servers isolated in private subnets.
3. **Hybrid Cloud Connectivity**
   - Connect corporate data centers to AWS.
4. **Multi-tier Architecture**
   - Separate presentation, application, and data layers.
5. **Disaster Recovery Setup**
   - Use multiple AZs for high availability and fault tolerance.

---

## 🧱 Best Practices

1. **Plan CIDR Blocks Carefully**
   - Avoid overlap with on-premise or other VPCs.
2. **Use Multiple Availability Zones**
   - For redundancy and fault tolerance.
3. **Apply Least Privilege Access**
   - Use fine-grained security rules.
4. **Separate Environments**
   - Create dedicated VPCs for Dev, Test, and Production.
5. **Enable Flow Logs**
   - For monitoring and troubleshooting.
6. **Use VPC Endpoints**
   - For private connectivity to AWS services.
7. **Restrict Inbound SSH**
   - Use bastion host or VPN instead.
8. **Regularly Review Security Rules**
   - Keep them minimal and up-to-date.

---

## 🧠 Practical Example: Deploying a 2-Tier Application in a Custom VPC

### Scenario:
You want to host a **web application** where:
- Web Server (EC2) is **publicly accessible**
- Database (RDS) is **private**

### Steps:

#### 1. Create VPC
- Name: `Prod-VPC`
- CIDR: `10.0.0.0/16`

#### 2. Create Subnets
- `10.0.1.0/24` → Public Subnet (Web)
- `10.0.2.0/24` → Private Subnet (DB)

#### 3. Internet Gateway
- Create and attach `Prod-IGW` to VPC.
- Update **Public Route Table**: `0.0.0.0/0 → IGW`.

#### 4. NAT Gateway
- Place in the Public Subnet.
- Update **Private Route Table**: `0.0.0.0/0 → NAT Gateway`.

#### 5. Security Groups
- **Web-SG**: Allow inbound HTTP (80), SSH (22).
- **DB-SG**: Allow inbound MySQL (3306) only from Web-SG.

#### 6. Launch Instances
- EC2 instance (Web Server) → Public Subnet.
- RDS instance (Database) → Private Subnet.

#### 7. Test
- Access EC2 via browser/public IP.
- Web app connects securely to private RDS through internal networking.

✅ You now have a **secure, multi-tier VPC architecture**.

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

---
