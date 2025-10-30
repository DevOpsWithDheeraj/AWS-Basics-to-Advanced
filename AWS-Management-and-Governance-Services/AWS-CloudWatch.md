# 🔍 **Amazon CloudWatch — Monitoring and Observability**

## 🧠 **What is Amazon CloudWatch?**

**Amazon CloudWatch** is a **monitoring and observability service** by AWS that collects and analyzes **metrics, logs, and events** from AWS resources, applications, and services.

It helps you gain **real-time visibility** into your infrastructure performance, resource utilization, and operational health.

> 💡 In simple terms:
> CloudWatch = “The Eyes of AWS” — it watches your infrastructure and applications in real time.

---

## ⚙️ 1. **Purpose**

CloudWatch helps you:

* **Monitor performance metrics** (CPU, memory, latency, etc.)
* **Collect and analyze logs**
* **Set alarms and notifications**
* **Automate responses to changes**
* **Visualize data using dashboards**
* **Detect and respond to anomalies**

---

## 🧩 2. **Key Components of CloudWatch**

| **Component**         | **Description**                                                                       |
| --------------------- | ------------------------------------------------------------------------------------- |
| **Metrics**           | Numerical data representing resource performance (e.g., CPUUtilization, DiskReadOps). |
| **Alarms**            | Trigger automated actions or notifications based on thresholds.                       |
| **Logs**              | Collect and store application/system logs for analysis.                               |
| **Dashboards**        | Custom visual interfaces to view metrics in real time.                                |
| **Events / Rules**    | Respond automatically to system events using Lambda, SNS, or Step Functions.          |
| **Anomaly Detection** | Uses ML to detect unusual patterns in metrics automatically.                          |

---

## 🪜 3. **How CloudWatch Works**

1. **Data Collection**
   CloudWatch collects **metrics and logs** from AWS services (EC2, RDS, Lambda, EKS, etc.) and custom sources (your own applications).

2. **Monitoring & Analysis**
   You can **view metrics**, **filter logs**, and **analyze performance** in the CloudWatch console.

3. **Automation via Alarms & Events**
   Set up **alarms** that trigger **SNS notifications**, **Auto Scaling actions**, or **Lambda functions** when thresholds are crossed.

4. **Visualization**
   Use **dashboards** to view performance metrics and health indicators in real time.

---

## 🧠 4. **Types of Monitoring**

| **Type**                | **Description**                                    | **Example**                                    |
| ----------------------- | -------------------------------------------------- | ---------------------------------------------- |
| **Basic Monitoring**    | Default metrics sent every 5 minutes for free.     | EC2 instance CPU, network, disk metrics.       |
| **Detailed Monitoring** | Metrics sent every 1 minute (paid).                | For critical production workloads.             |
| **Custom Metrics**      | User-defined metrics from applications or scripts. | Track number of user logins, queue depth, etc. |

---

## 💡 5. **Examples**

### 🧱 **Example 1: EC2 CPU Utilization Monitoring**

You have an EC2 instance running a web app.
You want to monitor **CPU usage** and get an alert when it’s above 80%.

**Steps:**

1. CloudWatch automatically collects **CPUUtilization** metrics.
2. You create an **Alarm**:

   * Condition: `CPUUtilization > 80% for 5 minutes`
   * Action: Send an **SNS notification** or trigger **Auto Scaling**.

📘 **Outcome:**
If CPU > 80% for 5 mins → CloudWatch sends an alert or adds another EC2 instance via Auto Scaling.

---

### 🌐 **Example 2: Monitoring Application Logs**

You have an application running on EC2 that writes logs to `/var/log/app.log`.
You want to monitor for the word “ERROR”.

**Steps:**

1. Install **CloudWatch Agent** on EC2 to push logs to **CloudWatch Logs**.
2. Create a **Metric Filter** for “ERROR”.
3. Create an **Alarm** when the count of “ERROR” exceeds 5 in 10 minutes.

📘 **Outcome:**
CloudWatch detects frequent errors and sends an alert → helps troubleshoot application issues in real time.

---

### ⚡ **Example 3: Automated Response to Failures**

Your web application’s **ELB (Elastic Load Balancer)** health check fails for multiple instances.

**Steps:**

1. CloudWatch receives the **UnhealthyHostCount** metric from ELB.
2. You create an **Event Rule**:

   * When ELB detects unhealthy instances → trigger an **AWS Lambda function**.
   * Lambda automatically restarts the failed instances.

📘 **Outcome:**
Automatic remediation — no manual action needed.

---

### 📊 **Example 4: Visual Dashboard for Multi-Service Monitoring**

You create a **CloudWatch Dashboard** to monitor:

* EC2 CPU & memory
* RDS connections
* S3 bucket requests
* Lambda invocation errors

📘 **Outcome:**
Centralized view of application health across all AWS services — ideal for DevOps teams during daily monitoring or incident response.

---

## 🧭 6. **Integration with Other AWS Services**

| **Service**          | **Integration Purpose**                                |
| -------------------- | ------------------------------------------------------ |
| **AWS Auto Scaling** | Automatically scale instances based on metrics.        |
| **AWS Lambda**       | Execute custom functions on alarms/events.             |
| **Amazon SNS**       | Send notifications to email, SMS, or Slack.            |
| **AWS CloudTrail**   | Combine logs for auditing user actions.                |
| **AWS Config**       | Correlate configuration changes with metric anomalies. |

---

## 🛠️ 7. **Benefits of CloudWatch**

| **Benefit**                | **Description**                                     |
| -------------------------- | --------------------------------------------------- |
| **Centralized Monitoring** | Monitor all AWS resources from one console.         |
| **Proactive Alerting**     | Detect and respond before failures occur.           |
| **Automated Remediation**  | Automatically fix or respond to events.             |
| **Scalable & Serverless**  | Works across multiple accounts and regions.         |
| **Cost Optimization**      | Identify underused or overused resources.           |
| **Custom Insights**        | Build dashboards and reports tailored to your team. |

---

## 🚀 8. **Real-World DevOps Use Case**

As a **DevOps Engineer at Infosys**, you’re responsible for maintaining uptime of a production web app.

You configure:

* **CloudWatch Metrics** to monitor EC2, RDS, and ELB performance.
* **CloudWatch Alarms** to trigger **SNS alerts** if CPU or latency spikes.
* **CloudWatch Dashboards** to visualize service health for your daily stand-up.
* **CloudWatch Logs Insights** to query error logs directly from the console.

✅ **Result:**
You gain **real-time operational visibility**, reduce downtime, and can **proactively respond to incidents** — without manual monitoring.

---

## 🧾 9. **Summary Table**

| **Feature**           | **Description**                             | **Example Use Case**                    |
| --------------------- | ------------------------------------------- | --------------------------------------- |
| **Metrics**           | Collect performance data from AWS resources | Track EC2 CPU and memory usage          |
| **Alarms**            | Trigger actions when thresholds are crossed | Send SNS alerts when CPU > 80%          |
| **Logs**              | Store and analyze system/application logs   | Monitor “ERROR” patterns in logs        |
| **Dashboards**        | Visualize metrics in real time              | Create a single view for EC2 + RDS      |
| **Events/Rules**      | Automate responses to system changes        | Restart instances via Lambda on failure |
| **Anomaly Detection** | Detect unusual metric behavior              | Identify sudden traffic spikes          |

---
