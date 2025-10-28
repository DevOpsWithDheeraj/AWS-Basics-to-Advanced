## 🧩 **EC2 Auto Scaling Group (ASG)**

---

### 🔹 **What is an Auto Scaling Group (ASG)?**

An **Auto Scaling Group (ASG)** in AWS automatically manages a group of **EC2 instances** based on demand.
It ensures that your application **always has the right number of instances** running — scaling **out (adding instances)** when traffic increases and **scaling in (removing instances)** when demand drops.

---

### ⚙️ **Key Components of ASG**

| Component                                  | Description                                                                     | Example                                          |
| ------------------------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------ |
| **Launch Template / Launch Configuration** | Defines how new EC2 instances are launched (AMI, instance type, key pair, etc.) | AMI = Amazon Linux 2, t3.micro, Key = my-keypair |
| **Minimum Size**                           | The minimum number of instances that should always be running                   | 2                                                |
| **Desired Capacity**                       | The target number of instances that should normally be running                  | 3                                                |
| **Maximum Size**                           | The maximum number of instances ASG can scale up to                             | 5                                                |
| **Scaling Policy**                         | Rules to decide when to add/remove instances                                    | Scale out if CPU > 70% for 5 mins                |
| **Health Checks**                          | Ensures only healthy instances are running                                      | EC2 + ELB Health Check                           |

---

### 🌐 **Example Scenario: A Web Application**

**Use Case:**
You have a web application running behind an **Application Load Balancer (ALB)**.
During daytime traffic spikes, you want more EC2 instances to handle the load.
At night, when traffic drops, you want fewer instances to save cost.

---

### 🏗️ **Step-by-Step Example Setup**

1. **Create a Launch Template**

   * Name: `webserver-template`
   * AMI: `Amazon Linux 2`
   * Instance Type: `t3.micro`
   * User Data: Script to install Apache web server

     ```bash
     #!/bin/bash
     yum install -y httpd
     systemctl start httpd
     echo "Hello from EC2 instance $(hostname)" > /var/www/html/index.html
     ```

2. **Create an Auto Scaling Group**

   * Name: `webserver-asg`
   * Launch Template: `webserver-template`
   * Min: 2, Desired: 3, Max: 5
   * Attach to **Load Balancer Target Group** (for traffic distribution)
   * Availability Zones: `us-east-1a`, `us-east-1b`

3. **Add Scaling Policies**

   * **Scale Out Policy:** Add 1 instance if average CPU > 70% for 5 minutes
   * **Scale In Policy:** Remove 1 instance if average CPU < 30% for 5 minutes

4. **Test Scaling**

   * Simulate traffic → CPU rises → ASG launches more EC2s.
   * When traffic drops → CPU falls → ASG terminates extra EC2s automatically.

---

### 📊 **Example in Real Numbers**

| Time  | CPU Utilization | Action Taken by ASG     | Instance Count |
| ----- | --------------- | ----------------------- | -------------- |
| 9 AM  | 25%             | No change               | 3              |
| 11 AM | 80%             | Scale out (+1 instance) | 4              |
| 1 PM  | 85%             | Scale out (+1 instance) | 5              |
| 10 PM | 20%             | Scale in (-2 instances) | 3              |

---

### 💡 **Real-World Use Case Example**

* **E-commerce Site:** Auto Scales during Black Friday sales to handle high user traffic.
* **News Website:** Auto Scales during breaking news spikes.
* **Gaming App Backend:** Automatically scales game servers during peak gaming hours.

---

### ✅ **Benefits of ASG**

* **High Availability** – Ensures minimum number of instances always running.
* **Cost Optimization** – Removes idle instances automatically.
* **Fault Tolerance** – Replaces unhealthy instances automatically.
* **Elasticity** – Adapts to workload changes in real-time.

---

### 🔸 **Summary Table**

| Feature             | Description                                   | Example                   |
| ------------------- | --------------------------------------------- | ------------------------- |
| **ASG Purpose**     | Automatically adjusts number of EC2 instances | Scale up/down web servers |
| **Scaling Trigger** | CloudWatch metrics like CPU, Memory, Network  | Scale out when CPU > 70%  |
| **Integration**     | Works with Load Balancer, CloudWatch          | ALB + ASG + CloudWatch    |
| **Main Benefit**    | Cost efficiency & high availability           | Save cost during low load |

---
