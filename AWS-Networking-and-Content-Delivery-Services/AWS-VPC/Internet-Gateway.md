## 🌐 What is an Internet Gateway (IGW)?

An **Internet Gateway** is a **horizontally scaled, highly available AWS-managed gateway** that allows communication between resources in your **VPC** and the **public Internet**.

In simple words —
🔹 It acts as a **bridge** between your **VPC** and the **Internet**.

Without an Internet Gateway, **your VPC is completely isolated** — no instance can send or receive data from the Internet.

---

## ⚙️ Key Features

| Feature                   | Description                                                                                                 |
| ------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Fully managed**         | You don’t need to configure or scale it manually — AWS handles that.                                        |
| **Highly available**      | It’s built for redundancy and doesn’t create a single point of failure.                                     |
| **Free of charge**        | No cost for creating or using it (you only pay for data transfer).                                          |
| **Two-way communication** | Supports both **inbound** (from Internet to instance) and **outbound** (from instance to Internet) traffic. |
| **Attached at VPC level** | One Internet Gateway can be attached to only one VPC at a time.                                             |

---

## 🧩 How Internet Gateway Works in AWS

### 1️⃣ Create a VPC

Let’s say your VPC has CIDR block:
`10.0.0.0/16`

### 2️⃣ Create a Subnet

You create a **Public Subnet**:
`10.0.1.0/24`

### 3️⃣ Create an Internet Gateway

You create an IGW (e.g., `igw-12345`) and **attach** it to your VPC.

### 4️⃣ Create a Route Table

You associate the **Public Subnet** with a **Route Table** that includes:

```
Destination: 0.0.0.0/0
Target: igw-12345
```

👉 This route means: “send all non-local traffic (Internet traffic) to the IGW.”

### 5️⃣ Assign a Public IP

Any EC2 instance in this subnet must have a **public IPv4 address or Elastic IP**.
This allows it to be reachable from the Internet.

✅ Now your EC2 instance can:

* **Send** data to the Internet (e.g., download updates).
* **Receive** data from the Internet (e.g., handle website requests).

---

## 🧠 Important Concepts

| Concept                     | Description                                                                                                                                   |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **IGW Attachment**          | An Internet Gateway must be attached to a VPC to function.                                                                                    |
| **Public IP Requirement**   | Instances need a public or Elastic IP to communicate with the Internet through IGW.                                                           |
| **Route Table Association** | Subnets must have a route pointing to the IGW for Internet access.                                                                            |
| **Stateful Nature**         | IGW is stateful — if a connection is initiated by an instance, the response traffic is automatically allowed, even if inbound rules block it. |
| **One-to-One Relationship** | One IGW can be attached to only one VPC at a time.                                                                                            |

---

## 🌍 Example Architecture

```
                 Internet
                     │
              [Internet Gateway]
                     │
        ┌───────────────────────────┐
        │        AWS VPC            │
        │     10.0.0.0/16           │
        │                           │
┌────────────┐             ┌────────────┐
│ Public RT  │             │ Private RT │
│ Route:     │             │ Route:     │
│ 0.0.0.0/0 → IGW          │ 0.0.0.0/0 → NAT │
└────────────┘             └────────────┘
     │                           │
 [Public Subnet]           [Private Subnet]
 (Web Server EC2)           (DB Server EC2)
```

In this setup:

* The **Public Subnet** uses IGW for direct Internet access.
* The **Private Subnet** uses a **NAT Gateway** to reach the Internet **outbound only**.

---

## 🔄 How IGW Handles Traffic

| Direction                     | Description                                                                               |
| ----------------------------- | ----------------------------------------------------------------------------------------- |
| **Outbound (VPC → Internet)** | EC2 sends packets → Route Table sends to IGW → IGW translates and sends to Internet.      |
| **Inbound (Internet → VPC)**  | Internet sends packets → IGW routes to EC2 instance (only if Security Group/NACL allows). |

---

## 🔒 Security Considerations

✅ **Security Groups** — Must allow inbound/outbound Internet traffic (e.g., port 80 or 443 for HTTP/HTTPS).
✅ **Network ACLs** — Must permit inbound/outbound traffic for Internet ports.
✅ **Public IPs** — Required for external reachability.
✅ **Least Privilege** — Only assign IGW routes to subnets that need Internet access.

---

## 🧾 Quick Summary Table

| Concept                   | Description                                       |
| ------------------------- | ------------------------------------------------- |
| **Definition**            | A gateway that connects your VPC to the Internet. |
| **Attachment**            | Must be attached to a VPC.                        |
| **Route Table**           | Public subnets have a route `0.0.0.0/0 → IGW`.    |
| **Public IP Requirement** | EC2 instances need a public or Elastic IP.        |
| **Stateful**              | Return traffic is automatically allowed.          |
| **Cost**                  | Free (pay only for data transfer).                |

---

## 💡 Real-World Example

Let’s say you’re hosting a website on EC2 in a **Public Subnet**.

* VPC CIDR: `10.0.0.0/16`
* Subnet CIDR: `10.0.1.0/24`
* Route Table: `0.0.0.0/0 → igw-12345`
* EC2: `10.0.1.10` with Public IP `54.120.15.25`

Now, when a user enters your website URL in their browser:

1. The DNS resolves to `54.120.15.25`.
2. Traffic flows from the Internet → IGW → EC2.
3. Your EC2 instance responds → IGW sends the response back to the Internet.

Result ✅: Your website is live and reachable globally.

---
