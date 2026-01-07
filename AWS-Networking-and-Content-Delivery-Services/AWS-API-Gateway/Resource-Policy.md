## What is a **Resource Policy** in AWS API Gateway?

A **Resource Policy** in **AWS API Gateway** is a **JSON-based policy** (similar to an IAM policy) that controls **who can access your API and from where**, **before** the request reaches backend integration (Lambda, EC2, etc.).

👉 In simple words:
**Resource Policy = “Gatekeeper of the API”**

---

## Why Resource Policy is Needed

Resource policy is mainly used to:

* Restrict API access to **specific AWS accounts**
* Restrict access based on **IP address**
* Allow only **VPC / VPC Endpoint** access (private API)
* Block public internet access

📌 **Applies at API level**, not per method.

---

## Where Resource Policy Works in API Flow

```
Client Request
   ↓
API Gateway Resource Policy  ← (Checked first)
   ↓
Authorization (IAM / Lambda / Cognito)
   ↓
Integration (Lambda / EC2 / HTTP)
```

---

## Resource Policy vs IAM Policy (Quick Difference)

| Feature     | Resource Policy    | IAM Policy            |
| ----------- | ------------------ | --------------------- |
| Attached to | API Gateway        | User / Role           |
| Controls    | Who can access API | What user can do      |
| Evaluated   | First              | After resource policy |
| Scope       | API-wide           | Identity-based        |

---

## Example 1: **Allow Access Only from Specific IP Address**

👉 Scenario:
Only your office IP should access the API.

### Resource Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "execute-api:Invoke",
      "Resource": "arn:aws:execute-api:us-east-1:123456789012:abcd1234/*/*/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "203.0.113.10/32"
        }
      }
    }
  ]
}
```

🔹 Only requests from `203.0.113.10` can access the API
🔹 All others get **403 Forbidden**

---

## Example 2: **Deny Public Access (Allow Only One AWS Account)**

👉 Scenario:
Only another AWS account (e.g., partner account) can call your API.

### Resource Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::999999999999:root"
      },
      "Action": "execute-api:Invoke",
      "Resource": "arn:aws:execute-api:us-east-1:123456789012:abcd1234/*"
    }
  ]
}
```

🔹 Only AWS account `999999999999` can access
🔹 Even if someone knows the API URL → **access denied**

---

## Example 3: **Allow Access Only from VPC Endpoint (Private API)**

👉 Scenario:
Your API should be accessible **only from inside a VPC**.

### Resource Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "execute-api:Invoke",
      "Resource": "arn:aws:execute-api:us-east-1:123456789012:abcd1234/*",
      "Condition": {
        "StringEquals": {
          "aws:SourceVpce": "vpce-0abc1234def567890"
        }
      }
    }
  ]
}
```

🔹 API accessible only via that **VPC Endpoint**
🔹 Requests from public internet → **Blocked**

---

## Example 4: **Block One IP, Allow Everyone Else**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Principal": "*",
      "Action": "execute-api:Invoke",
      "Resource": "*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "198.51.100.0/24"
        }
      }
    }
  ]
}
```

🔹 Useful to block malicious IP ranges
🔹 `Deny` always overrides `Allow`

---

## Important Rules to Remember

✔ Resource policy applies to **entire API**
✔ Evaluated **before authorizers**
✔ Works with **REST API & HTTP API**
✔ `Deny` always wins over `Allow`
✔ Mandatory for **Private API**

---

## Real-World DevOps Use Cases

| Use Case     | Why Resource Policy            |
| ------------ | ------------------------------ |
| Internal API | Restrict by VPC Endpoint       |
| Partner API  | Allow specific AWS account     |
| Security     | IP whitelisting                |
| Compliance   | Block public internet          |
| Cost control | Prevent unauthorized API calls |

---

## One-Line Summary (Interview Ready)

> **Resource Policy in API Gateway controls who can access the API and from where, at the API level, before any authorization or backend processing happens.**

---
