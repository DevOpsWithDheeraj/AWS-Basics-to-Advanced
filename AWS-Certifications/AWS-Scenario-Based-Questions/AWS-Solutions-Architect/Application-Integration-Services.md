
## 1️⃣ Amazon SQS – Decoupling Microservices

**Scenario:**
An e-commerce application uses multiple microservices. During flash sales, the order-processing service gets overwhelmed and causes failures in the payment service. The architect wants to **decouple services** and ensure **no messages are lost**, even during traffic spikes.

**Which solution is MOST appropriate?**

A. Use Amazon SNS with email notifications <br>
B. Use Amazon SQS Standard Queue between services <br>
C. Use AWS Step Functions to orchestrate services <br>
D. Use Amazon EventBridge with a custom event bus <br>

✅ **Correct Answer:** **B**

**Explanation:**

* **Amazon SQS Standard Queue** allows **asynchronous message processing**, decoupling services.
* It provides **high throughput and durability**, ideal for unpredictable spikes.
* SNS is for pub/sub, not message buffering.
* Step Functions orchestrate workflows, not buffering traffic.
* EventBridge is event-driven but not ideal for heavy message buffering.

---

## 2️⃣ Amazon SNS – Fan-Out Architecture

**Scenario:**
A media application publishes video upload events. These events must be processed by **multiple subscribers**, including:

* An email notification service
* A Lambda function for metadata extraction
* An SQS queue for analytics

**Which service should be used?**

A. Amazon SQS FIFO <br>
B. AWS Step Functions <br>
C. Amazon SNS <br>
D. Amazon EventBridge <br>

✅ **Correct Answer:** **C**

**Explanation:**

* **Amazon SNS** supports **fan-out messaging**, sending one message to multiple subscribers.
* It can deliver messages to **Lambda, SQS, HTTP, email**, etc.
* SQS alone does not support multiple consumers easily.
* Step Functions are for workflows.
* EventBridge is better for SaaS and service events, not direct fan-out.

---

## 3️⃣ SQS FIFO – Exactly-Once Processing

**Scenario:**
A financial transaction system must ensure that **each transaction is processed exactly once and in order**.

**Which solution meets this requirement?**

A. Amazon SQS Standard Queue <br>
B. Amazon SNS with message filtering <br>
C. Amazon SQS FIFO Queue <br>
D. Amazon EventBridge <br>

✅ **Correct Answer:** **C**

**Explanation:**

* **SQS FIFO** guarantees:

  * **Exactly-once processing**
  * **Strict message ordering**
* Standard queues offer at-least-once delivery and possible duplicates.
* SNS and EventBridge do not guarantee strict ordering.

---

## 4️⃣ AWS Step Functions – Workflow Orchestration

**Scenario:**
An application needs to coordinate multiple AWS Lambda functions:

* Validate input
* Process payment
* Update inventory
* Send confirmation

Each step must be retried on failure, and the entire workflow must be visually monitored.

**Which service should be used?**

A. Amazon SQS <br>
B. Amazon SNS <br>
C. AWS Step Functions <br>
D. Amazon EventBridge <br>

✅ **Correct Answer:** **C**

**Explanation:**

* **AWS Step Functions** are designed for **orchestrating distributed workflows**.
* They provide **state management, retries, error handling, and visual workflows**.
* SQS and SNS do not manage execution flow.
* EventBridge is event-driven, not workflow-oriented.

---

## 5️⃣ Amazon EventBridge – Event-Driven Architecture

**Scenario:**
A company wants to react to **AWS service events** (such as EC2 state changes) and **third-party SaaS events** (like Zendesk). The solution must use **rules to route events** to different targets.

**Which service should be used?**

A. Amazon SNS <br> 
B. Amazon SQS <br>
C. AWS Step Functions <br>
D. Amazon EventBridge <br>

✅ **Correct Answer:** **D**

**Explanation:**

* **Amazon EventBridge** is built for **event-driven architectures**.
* Supports:

  * AWS service events
  * Custom application events
  * SaaS partner events
* SNS is simpler pub/sub without advanced routing rules.

---

## 6️⃣ Dead-Letter Queue (DLQ) – Failure Handling

**Scenario:**
Messages in an SQS queue sometimes fail processing after multiple retries. The architect wants to **store failed messages for later analysis** without blocking the main queue.

**What should be configured?**

A. Increase message retention period <br>
B. Enable long polling <br>
C. Configure a Dead-Letter Queue (DLQ) <br>
D. Use Amazon SNS instead <br>

✅ **Correct Answer:** **C**

**Explanation:**

* A **Dead-Letter Queue (DLQ)** captures messages that exceed retry limits.
* Prevents poison messages from blocking processing.
* Retention and polling do not isolate failures.

---

## 7️⃣ Choosing Between SNS and EventBridge

**Scenario:**
An application must notify multiple internal systems when a new user registers. The message format is simple and does not require complex filtering or SaaS integrations.

**Which is the BEST choice?**

A. Amazon EventBridge <br>
B. Amazon SNS <br>
C. Amazon SQS FIFO <br>
D. AWS Step Functions <br>

✅ **Correct Answer:** **B**

**Explanation:**

* **SNS** is ideal for **simple pub/sub notifications**.
* EventBridge is better for complex routing and cross-service integrations.
* FIFO queues and Step Functions are unnecessary here.

---

## 8️⃣ Long Polling in SQS

**Scenario:**
An application continuously polls an SQS queue and incurs high API costs due to empty responses.

**How can costs be reduced?**

A. Increase message size <br>
B. Enable short polling <br>
C. Enable long polling <br>
D. Use FIFO queue <br>

✅ **Correct Answer:** **C**

**Explanation:**

* **Long polling** waits until a message arrives or timeout occurs.
* Reduces:

  * Empty responses
  * API calls
  * Cost
* Short polling increases empty responses.

---

### 📌 Exam Tip for SAA-C03

* **SQS** → Decoupling & buffering
* **SNS** → Fan-out & notifications
* **Step Functions** → Orchestration & workflows
* **EventBridge** → Event-driven & SaaS integration

---
