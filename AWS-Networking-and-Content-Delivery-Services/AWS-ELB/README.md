## What is Elastic Load Balancer (ELB)?

**Elastic Load Balancer (ELB)** is an AWS managed service that **automatically distributes incoming traffic across multiple targets** (EC2 instances, containers, IPs, Lambda) in one or more Availability Zones.
Its main goal is **high availability, scalability, and fault tolerance**.

---

## Why ELB is needed?

Without ELB:

* Users directly access one EC2 instance
* If that EC2 fails → application goes down
* Traffic spikes → instance overload

With ELB:

* Traffic is shared across multiple healthy targets
* Failed targets are automatically removed
* New targets are automatically added

---

## Key Functions of ELB

1. **Traffic distribution**
2. **Health checks**
3. **High availability (Multi-AZ)**
4. **Auto scaling integration**
5. **SSL/TLS termination**
6. **Security (works with SG, WAF, Shield)**

---

## Types of Elastic Load Balancers

| Type                                | Best For                               | Layer                |
| ----------------------------------- | -------------------------------------- | -------------------- |
| **Application Load Balancer (ALB)** | HTTP/HTTPS, microservices, containers  | Layer 7              |
| **Network Load Balancer (NLB)**     | High performance, TCP/UDP, low latency | Layer 4              |
| **Gateway Load Balancer (GWLB)**    | Firewalls, IDS/IPS appliances          | Layer 3              |
| **Classic Load Balancer (CLB)**     | Legacy applications                    | Layer 4 & 7 (legacy) |

---

## 1️⃣ Application Load Balancer (ALB)

### Features

* Works at **Layer 7 (HTTP/HTTPS)**
* **Path-based routing** (`/api`, `/images`)
* **Host-based routing** (`api.example.com`)
* Supports **containers (ECS, EKS)**
* WebSocket support

### Example – ALB with EC2

**Scenario:**
You have an e-commerce application.

```
User
  ↓
Application Load Balancer
  ↓
EC2-1 (AZ-1)
EC2-2 (AZ-2)
EC2-3 (AZ-3)
```

**Routing Rules:**

* `/products` → EC2 Target Group A
* `/orders` → EC2 Target Group B

**Flow:**

1. User hits `https://shop.example.com/products`
2. ALB checks routing rules
3. ALB forwards request to a **healthy EC2**
4. If EC2-2 fails → traffic goes to EC2-1 & EC2-3

---

## 2️⃣ Network Load Balancer (NLB)

### Features

* Works at **Layer 4 (TCP/UDP)**
* Handles **millions of requests/sec**
* Ultra-low latency
* Preserves **client IP**

### Example – NLB

**Scenario:** Real-time trading application

```
Client
  ↓ (TCP)
Network Load Balancer
  ↓
EC2 instances (Trading Engine)
```

**Why NLB?**

* Needs very low latency
* Handles massive concurrent connections

---

## 3️⃣ Gateway Load Balancer (GWLB)

### Features

* Deploy & scale **network appliances**
* Works with **firewalls, IDS, IPS**
* Uses **GENEVE protocol**

### Example – GWLB

```
Internet Traffic
   ↓
Gateway Load Balancer
   ↓
Firewall EC2 appliances
   ↓
Application
```

Used mainly in **security architectures**.

---

## Health Checks (Important Concept)

ELB sends periodic health check requests.

Example:

* Protocol: HTTP
* Path: `/health`
* Port: 80

If EC2 doesn’t respond →
❌ Marked **Unhealthy**
❌ Removed from traffic
✔ Traffic goes only to healthy instances

---

## ELB + Auto Scaling Example

```
User Traffic ↑
     ↓
Elastic Load Balancer
     ↓
Auto Scaling Group
     ↓
EC2 instances increase/decrease automatically
```

* High traffic → Auto Scaling adds EC2
* Low traffic → Auto Scaling removes EC2
* ELB automatically updates targets

---

## Security with ELB

* Works with **Security Groups**
* Integrates with **AWS WAF** (ALB only)
* Protected by **AWS Shield (DDoS protection)**
* Supports **HTTPS (SSL termination)**

---

## Real-Time Example (Interview Ready)

**Use Case:** Online Shopping Website

* ALB for HTTP/HTTPS traffic
* Auto Scaling Group with EC2
* Multi-AZ deployment
* HTTPS using ACM certificate

**Benefits:**

* Zero downtime
* Handles traffic spikes during sales
* Secure and scalable

---

## Summary

| Feature              | ELB |
| -------------------- | --- |
| Load distribution    | ✔   |
| High availability    | ✔   |
| Auto scaling support | ✔   |
| Health monitoring    | ✔   |
| Multiple LB types    | ✔   |

---
