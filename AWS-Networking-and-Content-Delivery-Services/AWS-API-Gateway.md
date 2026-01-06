
## **1️⃣ What is an API?**

**API (Application Programming Interface):**

* An **interface** that allows one software application to talk to another.
* Essentially, it **defines the rules** for requests and responses between systems.
* Think of it as a **menu in a restaurant**: you request a dish, and the kitchen (server) responds with the dish.

**Example:**

* When you use a mobile app to check the weather, it calls a weather API, which sends back the current temperature in JSON format.

---

## **2️⃣ What is an API Gateway?**

**API Gateway:**

* A **fully managed service** that acts as a **front door** for APIs to handle requests from clients and route them to backend services.
* It **abstracts backend complexity**, provides **security**, **rate limiting**, **caching**, **monitoring**, and **scaling**.

**Key uses:**

1. Expose AWS Lambda or EC2 APIs to clients.
2. Route requests to multiple backends.
3. Handle authentication, throttling, logging.

---

## **3️⃣ AWS API Gateway Components**

| Component                | Description                                                                                          |
| ------------------------ | ---------------------------------------------------------------------------------------------------- |
| **API**                  | The main container of resources and methods you expose. Can be REST API, HTTP API, or WebSocket API. |
| **Resource**             | Like a “path” in the URL (e.g., `/users`, `/orders`).                                                |
| **Method**               | HTTP methods like GET, POST, PUT, DELETE attached to resources.                                      |
| **Integration**          | Connects a method to a backend (Lambda, HTTP, Mock, or other AWS services).                          |
| **Stage**                | Version or environment of API (e.g., `dev`, `prod`).                                                 |
| **Deployment**           | Deploys the API to a stage.                                                                          |
| **Mapping Templates**    | Transform request or response payloads.                                                              |
| **Models**               | Define structure/schema for request or response (JSON Schema).                                       |
| **Authorizers**          | For authentication & authorization (Cognito, JWT, Lambda).                                           |
| **Throttling & Caching** | Control request rate and cache responses.                                                            |

---

## **4️⃣ Types of Requests (HTTP Methods)**

| HTTP Method | Usage                             | 
| ----------- | --------------------------------- |
| GET         | Retrieve/fetch data (read-only)        |
| POST        | Create new resource / submit / save data |
| PUT         | Update existing resource          |
| PATCH       | Partially update a resource       |
| DELETE      | Remove resource                   |

---

## **5️⃣ Proxy vs Non-Proxy Integration**

**1️⃣ Proxy Integration (Lambda Proxy / HTTP Proxy)**

* API Gateway **sends the full request to the backend** (headers, path, query string, body).
* Backend (e.g., Lambda) **handles everything**, including response formatting.
* Less configuration needed in API Gateway.

**Example Flow:**

```
Client → API Gateway → Lambda → API Gateway → Client
```

**2️⃣ Non-Proxy Integration**

* API Gateway **maps request data** to backend explicitly.
* You define **mapping templates** to transform incoming request.
* API Gateway can **manipulate response** before sending to client.

**Example Flow:**

```
Client → API Gateway → Mapping → Lambda → Mapping → Client
```

**When to use:**

* Proxy: Simple, direct, less configuration.
* Non-Proxy: Need transformation, validation, or multiple backends.

---

## **6️⃣ AWS Serverless Example: Lambda + API Gateway**

**Objective:** Create a simple API to return a welcome message.

**Step 1: Create Lambda Function**

```python
# Lambda Function: welcome_lambda.py
def lambda_handler(event, context):
    name = event.get("queryStringParameters", {}).get("name", "Guest")
    return {
        "statusCode": 200,
        "body": f"Hello, {name}! Welcome to Serverless API"
    }
```

**Step 2: Create API Gateway**

* Type: REST API (or HTTP API for simpler use)
* Resource: `/welcome`
* Method: `GET`
* Integration: Lambda Proxy Integration → select Lambda function

**Step 3: Deploy API**

* Stage: `dev`
* URL: `https://<api-id>.execute-api.<region>.amazonaws.com/dev/welcome?name=Dheeraj`

**Step 4: Test**

* Call URL via browser or Postman:

```
https://<api-id>.execute-api.<region>.amazonaws.com/dev/welcome?name=Dheeraj
```

* Response:

```json
"Hello, Dheeraj! Welcome to Serverless API"
```

✅ That’s it! You now have a **serverless API** with **AWS API Gateway + Lambda**.

---

