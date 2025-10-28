## 🌐 **Elastic Load Balancer (ELB)**

### 🔹 **What is ELB (Elastic Load Balancer)?**

**Elastic Load Balancer (ELB)** is an AWS service that automatically **distributes incoming traffic** across multiple **EC2 instances**, containers, IP addresses, or Lambda functions — to ensure:

* **High availability** (no single point of failure)
* **Scalability** (handles increased load automatically)
* **Fault tolerance** (routes traffic only to healthy targets)

Think of ELB as a **traffic manager** that decides **which EC2 instance** should handle each request.

---

### ⚙️ **Why Use ELB?**

Without a Load Balancer:

* Traffic goes directly to one EC2 → it can overload or fail.
* Manual scaling and failover are required.

With ELB:

* Traffic is automatically spread across multiple instances.
* Health checks ensure only healthy instances get traffic.
* You can integrate with **Auto Scaling Groups (ASG)** for elasticity.

---

### ⚖️ **Types of Elastic Load Balancers**

| ELB Type                               | Best For                                     | Protocols Supported  | Example                                                    |
| -------------------------------------- | -------------------------------------------- | -------------------- | ---------------------------------------------------------- |
| **1. Application Load Balancer (ALB)** | Web applications (HTTP/HTTPS), microservices | HTTP, HTTPS          | Routes requests to `/api` → backend1, `/images` → backend2 |
| **2. Network Load Balancer (NLB)**     | High-performance, low-latency apps           | TCP, UDP, TLS        | Routes database or gaming traffic                          |
| **3. Gateway Load Balancer (GLB)**     | Deploying firewalls or inspection appliances | IP (GENEVE protocol) | Routes traffic through security appliances                 |
| **4. Classic Load Balancer (CLB)**     | Legacy apps                                  | HTTP, HTTPS, TCP     | Older generation of ALB/NLB                                |

---

### 🧩 **1️⃣ Application Load Balancer (ALB) — Example**

#### 🧠 Use Case:

You have a web application hosted on multiple EC2 instances in two Availability Zones:

* `/api` → points to backend servers
* `/images` → points to image servers

#### 🏗️ Setup Steps:

1. **Create Target Groups**

   * `api-target-group` → contains EC2 instances for API
   * `images-target-group` → contains EC2 instances for image hosting

2. **Create ALB**

   * Name: `my-alb`
   * Type: Application Load Balancer
   * Scheme: Internet-facing
   * Listener: HTTP (port 80)

3. **Configure Rules**

   * If request path = `/api/*` → forward to `api-target-group`
   * If request path = `/images/*` → forward to `images-target-group`
   * Default → show “Homepage” from `default-target-group`

4. **Register Targets**

   * Add EC2 instances in each target group.

5. **Test**

   * `http://my-alb.amazonaws.com/api/users` → goes to API server
   * `http://my-alb.amazonaws.com/images/logo.png` → goes to image server

---

### ⚡ **2️⃣ Network Load Balancer (NLB) — Example**

#### 🧠 Use Case:

You run a real-time multiplayer gaming app that requires ultra-low latency and handles TCP connections directly.

#### 🏗️ Setup Steps:

1. Create **Target Group** (protocol: TCP, port: 3000)
2. Register EC2 instances (game servers)
3. Create an **NLB**

   * Type: Network Load Balancer
   * Listener: TCP 3000 → forward to the target group
4. Test using the NLB DNS:

   * `nlb-123456.elb.amazonaws.com:3000`

💡 **NLB Highlights:**

* Handles **millions of requests per second**
* Best for **IoT, VoIP, Financial apps, Gaming**

---

### 🔒 **3️⃣ Gateway Load Balancer (GLB) — Example**

#### 🧠 Use Case:

Your company uses third-party **firewall or intrusion detection** appliances.
You want traffic to automatically pass through them before reaching servers.

#### 🏗️ Setup Steps:

1. Deploy security appliances as EC2 instances.
2. Create a **Gateway Load Balancer** and register appliances as targets.
3. Use a **Gateway Load Balancer Endpoint (GWLBe)** in your VPC.
4. Route traffic through this endpoint → all packets inspected before reaching app.

---

### 🏛️ **4️⃣ Classic Load Balancer (CLB) — Legacy**

#### 🧠 Use Case:

Older apps built before 2016 using EC2-Classic network.

* Operates at **Layer 4 (TCP)** and **Layer 7 (HTTP/HTTPS)**.
* Not recommended for new applications.

---

### 💡 **How ELB Works (Simplified Flow)**

```
Client → ELB DNS → Load Balancer → Healthy EC2 Instance
```

If one EC2 instance fails:

```
ELB Health Check detects failure → stops sending traffic to that instance → routes to other healthy EC2s
```

---

### 📊 **Example: Web App with ASG + ELB**

| Component                     | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| **Launch Template**           | Defines EC2 instance setup (AMI, Apache, app code) |
| **Auto Scaling Group**        | Ensures min 2, max 5 EC2s running                  |
| **Application Load Balancer** | Distributes traffic across all EC2s                |
| **CloudWatch**                | Monitors CPU and triggers scaling                  |
| **Route 53**                  | Custom domain pointing to ALB DNS                  |

🧩 **Flow:**

1. User opens `https://myapp.com`
2. DNS (Route 53) → points to ALB
3. ALB → forwards request to healthy EC2 instance in ASG
4. If traffic spikes → ASG adds EC2s; ALB automatically includes new ones

---

### ✅ **Benefits of ELB**

| Benefit               | Explanation                                       |
| --------------------- | ------------------------------------------------- |
| **High Availability** | Routes traffic across multiple AZs                |
| **Fault Tolerance**   | Removes unhealthy instances automatically         |
| **Scalability**       | Integrates with Auto Scaling for elastic capacity |
| **Security**          | Supports HTTPS, SSL/TLS termination               |
| **Monitoring**        | Integrated with CloudWatch for metrics            |
| **Sticky Sessions**   | Optionally keep the same client on one instance   |

---

### 🧠 **Real-World Example**

**Company:** Netflix
**Use Case:** Streaming video across multiple EC2 instances globally.

* **ALB** routes HTTP(S) video requests
* **NLB** handles TCP for control & signaling
* **Auto Scaling** ensures enough backend instances
* **CloudWatch** monitors latency and errors

---

### 🧾 **Summary Table**

| Feature       | ALB                       | NLB                      | GLB                   | CLB              |
| ------------- | ------------------------- | ------------------------ | --------------------- | ---------------- |
| Layer         | 7 (HTTP/HTTPS)            | 4 (TCP/UDP)              | 3 (IP)                | 4 & 7            |
| Best For      | Web apps, microservices   | Gaming, IoT, finance     | Firewalls, inspection | Legacy apps      |
| Protocols     | HTTP, HTTPS               | TCP, UDP, TLS            | IP (GENEVE)           | HTTP, HTTPS, TCP |
| Health Checks | HTTP                      | TCP                      | IP                    | HTTP, TCP        |
| Cost          | Medium                    | Low                      | High                  | Low              |
| Example       | Web app with path routing | Real-time chat or gaming | Security inspection   | Old monolith app |

---
