
# 🔍 What are Validators in AWS API Gateway?

**Validators** in **AWS API Gateway** are used to **validate incoming client requests before they reach the backend** (Lambda / HTTP / AWS service).

They help ensure:

* Required **query parameters** are present
* Required **headers** are present
* **Request body** matches the defined **JSON schema (Model)**

👉 If validation fails, **API Gateway itself returns 400 Bad Request**, and **backend is NOT invoked**.

---

## ❓ Why Validators are Important

Without validators:

* Invalid data reaches Lambda
* You must write extra validation code
* More Lambda invocations = higher cost

With validators:

* Early rejection of bad requests
* Cleaner backend code
* Better API reliability

---

# 🧩 Types of Request Validators

API Gateway provides **3 validator options**:

| Validator Type                   | What It Validates                 |
| -------------------------------- | --------------------------------- |
| **Validate body**                | Request body against Model schema |
| **Validate parameters**          | Headers & Query string parameters |
| **Validate body and parameters** | Both body + params                |

---

# 📌 Example 1: Query Parameter Validation (Non-Proxy)

### Scenario

Client must send a query parameter `name`.

### Step 1: Define Method Request Parameters

**Method Request → URL Query String Parameters**

| Name | Required |
| ---- | -------- |
| name | ✅ true   |

---

### Step 2: Enable Validator

**Method Request → Request Validator**

```
Validate query string parameters and headers
```

---

### Request (Valid)

```
GET /hello?name=Dheeraj
```

✔ Passed → Sent to backend

---

### Request (Invalid)

```
GET /hello
```

❌ API Gateway Response:

```json
{
  "message": "Missing required request parameters: [name]"
}
```

➡️ Backend not invoked

---

# 📌 Example 2: Header Validation

### Scenario

Client must send header `x-api-key`.

### Method Request → Headers

| Header Name | Required |
| ----------- | -------- |
| x-api-key   | ✅ true   |

### Validator

```
Validate query string parameters and headers
```

---

### Invalid Request

```
GET /secure-api
```

❌ Response:

```json
{
  "message": "Missing required request parameters: [x-api-key]"
}
```

---

# 📌 Example 3: Request Body Validation (Using Models)

### Scenario

POST request with JSON body:

```json
{
  "name": "Dheeraj",
  "age": 25
}
```

---

### Step 1: Create a Model

**Models → Create Model**

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "required": ["name", "age"],
  "properties": {
    "name": {
      "type": "string"
    },
    "age": {
      "type": "integer"
    }
  }
}
```

---

### Step 2: Attach Model to Method

**Method Request → Request Body**

* Content-Type: `application/json`
* Model: `UserModel`

---

### Step 3: Enable Validator

```
Validate body
```

---

### Invalid Request

```json
{
  "name": "Dheeraj"
}
```

❌ Response:

```json
{
  "message": "Invalid request body"
}
```

---

# 📌 Example 4: Body + Parameter Validation (Most Used)

Validator:

```
Validate body and query string parameters and headers
```

✔ Ensures:

* Query params exist
* Headers exist
* Body schema is valid

This is **very common in production APIs**.

---

# 🔁 Validators vs Lambda Validation

| Feature             | API Gateway Validator | Lambda Code |
| ------------------- | --------------------- | ----------- |
| Runs before backend | ✅ Yes                 | ❌ No        |
| Reduces Lambda cost | ✅ Yes                 | ❌ No        |
| Easy configuration  | ✅ Yes                 | ❌ No        |
| Complex logic       | ❌ Limited             | ✅ Yes       |

👉 Best practice:
**Basic validation → API Gateway**
**Business validation → Lambda**

---

# ⚠️ Important Notes

* Validators **do NOT validate values**, only presence & structure
  ❌ Cannot check `age > 18`
* Works best with **Non-Proxy Integration**
* In **Proxy Integration**, body validation is limited (usually done in Lambda)

---

# 🧠 Real-World Use Case

**User Registration API**

* Validate `email`, `password`, `phone` exist → API Gateway
* Validate password strength → Lambda
* Save user → DynamoDB

---

