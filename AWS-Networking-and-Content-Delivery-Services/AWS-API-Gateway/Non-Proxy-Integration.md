
## What is **Non-Proxy Integration** in AWS API Gateway?

**Non-Proxy Integration** means:

> You **control how requests are sent to the backend** and **how responses are returned to the client** using **mapping templates**.

Unlike proxy integration, API Gateway **does NOT forward everything automatically**.

You must **manually define**:

* What data goes **from client → backend**
* What data goes **from backend → client**

---

## When do we use Non-Proxy Integration?

Use **Non-Proxy Integration** when you need:

✅ Modify request/response format
✅ Send only selected parameters to backend
✅ Transform JSON/XML
✅ Add prefixes, headers, static values
✅ Integrate with **legacy systems**
✅ Fine-grained control (common in enterprises)

---

## Supported Backends

Non-Proxy integration can be used with:

* **AWS Lambda**
* **HTTP / HTTPS backend**
* **AWS services** (SQS, DynamoDB, SNS, etc.)

---

## High-Level Flow

```
Client
  |
  v
API Gateway
  |  (Mapping Template)
  v
Backend (Lambda / HTTP / AWS Service)
  |
  v
API Gateway
  |  (Response Mapping)
  v
Client
```

---

## Example 1: Non-Proxy Integration with **Lambda**

### Scenario

Client sends:

```
POST /user?name=rahul
```

You want Lambda to receive:

```json
{
  "username": "rahul"
}
```

---

### Step 1: Create API Method

* API Gateway → Resource `/user`
* Method: **POST**
* Integration type: **Lambda (Non-Proxy)** ❌ (unchecked “Use Lambda Proxy integration”)

---

### Step 2: Request Mapping Template

**Content-Type:** `application/json`

```vtl
{
  "username": "$input.params('name')"
}
```

📌 What happens?

* Client sends `?name=rahul`
* Lambda receives:

```json
{
  "username": "rahul"
}
```

---

### Step 3: Lambda Code (Python)

```python
def lambda_handler(event, context):
    return {
        "message": f"Hello {event['username']}"
    }
```

---

### Step 4: Response Mapping Template

```vtl
{
  "result": "$input.path('$.message')"
}
```

---

### Final Response to Client

```json
{
  "result": "Hello rahul"
}
```

✔ Full control over request and response

---

## Example 2: Non-Proxy Integration with **HTTP Backend**

### Scenario

Client sends:

```json
{
  "name": "Dheeraj"
}
```

Backend API expects:

```json
{
  "user_name": "Dheeraj",
  "source": "api-gateway"
}
```

---

### Request Mapping Template

```vtl
{
  "user_name": "$input.json('$.name')",
  "source": "api-gateway"
}
```

✔ API Gateway transforms client request before sending

---

## Example 3: Non-Proxy Integration with **AWS SQS**

### Scenario

Send message to SQS from API Gateway

---

### Request Mapping Template

```vtl
Action=SendMessage&
MessageBody=$util.urlEncode($input.body)&
QueueUrl=https://sqs.ap-south-1.amazonaws.com/123456789012/my-queue
```

✔ Client doesn’t need to know SQS format
✔ API Gateway handles transformation

---

## Proxy vs Non-Proxy (Quick Comparison)

| Feature           | Proxy Integration | Non-Proxy Integration |
| ----------------- | ----------------- | --------------------- |
| Mapping templates | ❌ Not needed      | ✅ Mandatory           |
| Control over data | ❌ Limited         | ✅ Full                |
| Speed of setup    | ⭐⭐⭐⭐ Fast         | ⭐ Slower              |
| Flexibility       | ❌ Low             | ✅ High                |
| Use case          | Microservices     | Legacy / Enterprise   |

---

## Key Points to Remember (Interview ⭐)

* Non-Proxy = **Manual mapping**
* Uses **Velocity Template Language (VTL)**
* Request & Response **both need templates**
* More control but more configuration
* Good for **data transformation**

---

## Simple One-Line Definition

> **Non-Proxy integration allows API Gateway to transform requests and responses using mapping templates before sending data to backend services.**

---

