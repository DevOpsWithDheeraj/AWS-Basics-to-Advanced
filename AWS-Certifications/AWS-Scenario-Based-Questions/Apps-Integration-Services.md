
## 1️⃣ Decoupling application components

A company has a web application where the frontend sends requests to a backend processing service. The company wants to **decouple the two components** so that traffic spikes do not overload the backend.

Which AWS service should be used?

A. AWS Step Functions <br>
B. Amazon SQS <br>
C. Amazon SNS <br>
D. AWS AppSync <br>

✅ **Correct Answer: B. Amazon SQS**

**Explanation:**
Amazon SQS provides a **message queue** that decouples producers and consumers. The frontend can send messages to the queue, and the backend can process them at its own pace, handling traffic spikes efficiently.

---

## 2️⃣ Broadcasting messages to multiple systems

An e-commerce platform needs to send order notifications to **email, SMS, and analytics systems simultaneously** whenever an order is placed.

Which AWS service is BEST suited?

A. Amazon SQS <br>
B. AWS EventBridge <br>
C. Amazon SNS <br>
D. AWS Step Functions <br>

✅ **Correct Answer: C. Amazon SNS**

**Explanation:**
Amazon SNS uses a **publish–subscribe model**, allowing a single message to be sent to **multiple subscribers** at the same time, making it ideal for notifications.

---

## 3️⃣ Orchestrating multiple AWS services

A serverless application requires a workflow that:

* Invokes AWS Lambda
* Calls DynamoDB
* Handles retries and errors automatically

Which AWS service should be used?

A. Amazon SQS <br>
B. Amazon SNS <br>
C. AWS Step Functions <br>
D. Amazon EventBridge <br>

✅ **Correct Answer: C. AWS Step Functions**

**Explanation:**
AWS Step Functions is used for **orchestrating workflows** across multiple AWS services with built-in error handling, retries, and state management.

---

## 4️⃣ Event-driven architecture across AWS services

A company wants to automatically trigger different AWS services when specific AWS resource events occur, such as **EC2 instance state changes**.

Which service should they use?

A. Amazon SNS <br>
B. Amazon SQS <br>
C. AWS EventBridge <br>
D. AWS Step Functions <br>

✅ **Correct Answer: C. AWS EventBridge**

**Explanation:**
AWS EventBridge enables **event-driven architectures** by routing events from AWS services to targets like Lambda, SQS, or Step Functions.

---

## 5️⃣ Temporary message storage during traffic bursts

An application receives thousands of requests per second, but the backend can process only a limited number at a time. Messages must be **stored temporarily** until processed.

Which AWS service should be used?

A. Amazon SNS <br>
B. Amazon SQS <br>
C. AWS Step Functions <br>
D. Amazon EventBridge <br>

✅ **Correct Answer: B. Amazon SQS**

**Explanation:**
Amazon SQS acts as a **buffer** that stores messages until consumers are ready to process them, protecting backend services from overload.

---

## 6️⃣ Fan-out architecture requirement

A company wants to send a message to **multiple SQS queues and Lambda functions** at once.

Which service enables this pattern?

A. Amazon SNS <br>
B. Amazon SQS <br>
C. AWS Step Functions <br>
D. Amazon EventBridge <br>

✅ **Correct Answer: A. Amazon SNS**

**Explanation:**
Amazon SNS supports **fan-out messaging**, where a single published message can be delivered to multiple endpoints such as SQS queues, Lambda functions, or HTTP endpoints.

---

## 7️⃣ Simple event routing without workflow logic

An application needs to route events from one AWS service to another **without complex workflow logic**.

Which service is MOST appropriate?

A. AWS Step Functions <br>
B. Amazon SNS <br>
C. Amazon SQS <br>
D. AWS EventBridge <br>

✅ **Correct Answer: D. AWS EventBridge**

**Explanation:**
EventBridge focuses on **event routing and filtering**, not workflow orchestration, making it ideal for simple event-based integrations.

---

## 8️⃣ Ensuring message delivery even if consumer fails

A message must remain available until it is **successfully processed**, even if the consumer application crashes.

Which service ensures this behavior?

A. Amazon SNS <br>
B. Amazon SQS <br>
C. AWS EventBridge <br>
D. AWS Step Functions <br>

✅ **Correct Answer: B. Amazon SQS**

**Explanation:**
Amazon SQS retains messages until they are **explicitly deleted** by the consumer after successful processing.

---

## 🔑 Quick Exam Tip (Cloud Practitioner)

| Requirement             | Best Service           |
| ----------------------- | ---------------------- |
| Decoupling & buffering  | **Amazon SQS**         |
| Notifications & fan-out | **Amazon SNS**         |
| Workflow orchestration  | **AWS Step Functions** |
| Event-driven routing    | **Amazon EventBridge** |

---
