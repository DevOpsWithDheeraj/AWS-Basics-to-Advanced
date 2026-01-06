## What is Proxy Integration in AWS API Gateway?

**Proxy Integration** means:

> **API Gateway forwards the entire HTTP request to the backend (Lambda / HTTP service) as-is**, and the backend is responsible for **handling request parsing and building the response**.

👉 API Gateway does **minimal processing**
👉 **Backend controls everything**

---

## Types of Proxy Integration

API Gateway supports **two main proxy integrations**:

| Type                         | Used With            |
| ---------------------------- | -------------------- |
| **Lambda Proxy Integration** | AWS Lambda           |
| **HTTP Proxy Integration**   | HTTP / HTTPS backend |

---

# 1️⃣ Lambda Proxy Integration (Most Common)

### What happens?

* Client sends request → API Gateway
* API Gateway forwards **full request** to Lambda
* Lambda:

  * Reads path, query params, headers, body, method
  * Builds full HTTP response
* API Gateway returns Lambda response to client

---

## Request Flow (Simple)

```
Client
  ↓
API Gateway (Proxy)
  ↓
Lambda (business logic + response)
  ↓
API Gateway
  ↓
Client
```

---

## Example: Lambda Proxy Integration

### API Request (from Postman)

```
POST /users?id=101
Headers:
  Content-Type: application/json

Body:
{
  "name": "Dheeraj",
  "role": "DevOps"
}
```

---

### Event received by Lambda (IMPORTANT)

```json
{
  "resource": "/users",
  "path": "/users",
  "httpMethod": "POST",
  "headers": {
    "Content-Type": "application/json"
  },
  "queryStringParameters": {
    "id": "101"
  },
  "body": "{\"name\":\"Dheeraj\",\"role\":\"DevOps\"}",
  "isBase64Encoded": false
}
```

👉 Lambda receives **everything**
👉 No mapping templates needed

---

### Lambda Response (You must format this!)

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"User created successfully\"}"
}
```

---

### Final Response to Client

```json
{
  "message": "User created successfully"
}
```

---

## Key Points of Lambda Proxy Integration

✔ No request mapping
✔ No response mapping
✔ Faster development
✔ Less API Gateway configuration
❌ Lambda code slightly more complex

---

# 2️⃣ HTTP Proxy Integration

Used when API Gateway forwards requests to an **external HTTP backend**.

### Example Use Case

* API Gateway in front of:

  * On-prem service
  * EC2-hosted app
  * Third-party API

---

## Example: HTTP Proxy Integration

### API Gateway Endpoint

```
https://api.example.com/orders
```

### Backend Service

```
https://backend.example.com/orders
```

---

### Request Flow

```
Client → API Gateway → Backend HTTP Service → API Gateway → Client
```

API Gateway:

* Forwards:

  * HTTP method
  * Path
  * Headers
  * Query params
  * Body

---

### Client Request

```
GET /orders?status=shipped
```

### Backend Receives (Same request)

```
GET /orders?status=shipped
```

👉 No transformation
👉 No mapping templates

---

# Proxy vs Non-Proxy Integration (Quick Comparison)

| Feature                | Proxy Integration     | Non-Proxy Integration |
| ---------------------- | --------------------- | --------------------- |
| Request mapping        | ❌ Not required        | ✅ Required            |
| Response mapping       | ❌ Not required        | ✅ Required            |
| Control in API Gateway | ❌ Low                 | ✅ High                |
| Control in backend     | ✅ High                | ❌ Low                 |
| Complexity             | Low                   | High                  |
| Best for               | Microservices, Lambda | Legacy / strict APIs  |

---

## When Should You Use Proxy Integration?

✅ Modern serverless apps
✅ Microservices
✅ Rapid development
✅ DevOps / CI-CD pipelines
✅ When backend owns API logic

---

## When NOT to Use Proxy Integration?

❌ When you need:

* Heavy request transformation
* Different response formats per client
* Strict validation at API Gateway level

---

## Interview Tip (Very Important)

💡 **Most real-world projects use Lambda Proxy Integration**
💡 Non-proxy is mainly for **legacy or complex transformation needs**

---
