
## What is an Authorizer in AWS API Gateway?

An **Authorizer** controls **who can access your API**.

👉 It runs **before** your backend (Lambda / EC2 / HTTP service) is invoked.
👉 If authorization fails → API Gateway returns **401 / 403** immediately.
👉 If authorization succeeds → request is forwarded to the backend.

---

## Why Do We Need Authorizers?

Without an authorizer:

* Anyone who knows the API URL can call it ❌

With an authorizer:

* Only authenticated and authorized users can access it ✅

---

## Types of Authorizers in API Gateway

| Authorizer Type                | Used For                             |
| ------------------------------ | ------------------------------------ |
| **IAM Authorizer**             | AWS IAM users, roles, services       |
| **Lambda Authorizer (Custom)** | Custom logic (JWT, OAuth, DB lookup) |
| **Cognito Authorizer**         | User login using Amazon Cognito      |

---

# 1️⃣ IAM Authorizer

### What it does

Uses **AWS IAM** to authorize API requests.

### How it works (Flow)

```
Client → API Gateway → IAM Policy Check → Backend
```

### Example Use Case

* Internal microservices
* AWS CLI access
* EC2 / Lambda calling API Gateway

### Example: API call using IAM

```bash
aws apigateway invoke \
  --rest-api-id abc123 \
  --resource-id xyz456 \
  --http-method GET
```

IAM policy:

```json
{
  "Effect": "Allow",
  "Action": "execute-api:Invoke",
  "Resource": "arn:aws:execute-api:region:account-id:api-id/*/GET/myapi"
}
```

### Key Point

✅ No coding required
❌ Not suitable for public users

---

# 2️⃣ Lambda Authorizer (Custom Authorizer)

### What it does

Uses a **Lambda function** to validate requests.

You can:

* Validate JWT tokens
* Check API keys in DB
* Implement custom RBAC logic

---

## Types of Lambda Authorizers

| Type        | Input                              |
| ----------- | ---------------------------------- |
| **TOKEN**   | Authorization header               |
| **REQUEST** | Headers, query params, path params |

---

## Example 1: TOKEN-based Lambda Authorizer

### Flow

```
Client → API Gateway
        → Lambda Authorizer
        → Allow/Deny
        → Backend
```

### Client Request

```http
GET /orders
Authorization: Bearer abc123token
```

### Lambda Authorizer Code (Python)

```python
def lambda_handler(event, context):
    token = event['authorizationToken']

    if token == "Bearer valid-token":
        return {
            "principalId": "user123",
            "policyDocument": {
                "Version": "2012-10-17",
                "Statement": [{
                    "Action": "execute-api:Invoke",
                    "Effect": "Allow",
                    "Resource": event["methodArn"]
                }]
            }
        }
    else:
        raise Exception("Unauthorized")
```

### Response

* Valid token → 200 OK
* Invalid token → 401 Unauthorized

---

## Example 2: REQUEST-based Lambda Authorizer

### Client Request

```http
GET /orders?role=admin
X-API-KEY: 12345
```

### Lambda Authorizer Code

```python
def lambda_handler(event, context):
    role = event['queryStringParameters']['role']
    api_key = event['headers']['X-API-KEY']

    if role == "admin" and api_key == "12345":
        effect = "Allow"
    else:
        effect = "Deny"

    return {
        "principalId": "user1",
        "policyDocument": {
            "Version": "2012-10-17",
            "Statement": [{
                "Action": "execute-api:Invoke",
                "Effect": effect,
                "Resource": event["methodArn"]
            }]
        }
    }
```

---

## Caching in Lambda Authorizers

API Gateway can **cache authorization results**:

| Feature          | Benefit                  |
| ---------------- | ------------------------ |
| TTL (0–3600 sec) | Faster performance       |
| Same token reuse | Fewer Lambda invocations |

⚠️ If user permissions change frequently → disable caching.

---

# 3️⃣ Cognito Authorizer

### What it does

Uses **Amazon Cognito User Pools** to authenticate users.

### Flow

```
User → Login (Cognito)
     → JWT Token
     → API Gateway
     → Backend
```

### Example

1. User logs in → gets JWT token
2. Calls API:

```http
GET /profile
Authorization: Bearer eyJraWQiOi...
```

3. API Gateway:

* Validates JWT
* Checks token expiry
* Forwards request if valid

### Key Benefits

✅ No Lambda needed
✅ Built-in JWT validation
❌ Less flexible than Lambda Authorizer

---

## Comparison Table

| Feature       | IAM  | Lambda | Cognito |
| ------------- | ---- | ------ | ------- |
| Public APIs   | ❌    | ✅      | ✅       |
| Custom logic  | ❌    | ✅      | ❌       |
| JWT support   | ❌    | ✅      | ✅       |
| Performance   | High | Medium | High    |
| Ease of setup | Easy | Medium | Easy    |

---

## Real-World DevOps Scenarios (Important ⭐)

| Scenario                   | Best Authorizer |
| -------------------------- | --------------- |
| Internal AWS service calls | IAM             |
| Mobile/Web App with login  | Cognito         |
| Third-party API clients    | Lambda          |
| Fine-grained RBAC          | Lambda          |

---

## Key Interview Points (Remember This)

✔ Authorizers run **before integration**
✔ Lambda Authorizers return **IAM policy**
✔ Authorization ≠ Authentication
✔ Can be attached at **method level**

---
