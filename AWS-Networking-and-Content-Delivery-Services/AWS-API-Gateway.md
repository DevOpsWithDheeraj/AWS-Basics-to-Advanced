# 🌐 Amazon API Gateway 

## 📘 What is Amazon API Gateway?

**Amazon API Gateway** is a **fully managed service** that allows developers to **create, deploy, and manage APIs** at any scale.  
It acts as a **front door for applications** to access backend services such as **AWS Lambda, EC2, or any web application**, handling **request routing, throttling, security, and monitoring** automatically.

Key features:
- Create **RESTful, HTTP, and WebSocket APIs**
- Enable **authentication and authorization**
- Apply **throttling and quotas**
- Monitor API performance with **Amazon CloudWatch**
- Seamlessly integrate with **serverless architectures**

> Simply put, API Gateway is the **gateway between clients and your backend services**, scalable and secure.

---

## ⚙️ How to Configure Amazon API Gateway

### Step-by-Step Configuration:

1. **Open the API Gateway Console**
   - Navigate to **AWS Management Console → API Gateway → Create API**.

2. **Choose API Type**
   - **HTTP API** – Simplified, low-latency API
   - **REST API** – Full-featured API with advanced options
   - **WebSocket API** – For real-time communication

3. **Define API Settings**
   - API Name: `MyAppAPI`
   - Endpoint Type: `Regional`, `Edge-Optimized`, or `Private`

4. **Create Resources and Methods**
   - **Resource**: Path for the API (e.g., `/users`)
   - **Method**: HTTP verb (GET, POST, PUT, DELETE)
   - Connect method to **backend integration** (Lambda, HTTP endpoint, or Mock)

5. **Configure Security**
   - Use **IAM roles**, **Cognito user pools**, or **API keys**
   - Set **throttling and quotas** for usage control

6. **Deploy API**
   - Create a **Stage** (e.g., `dev`, `prod`)
   - Obtain **invoke URL** for client access

7. **Monitor API**
   - Enable **CloudWatch metrics and logs** to track usage, latency, and errors

---

## 🧩 Components of API Gateway

| Component | Description |
|------------|--------------|
| **API** | Container for all resources and methods |
| **Resource** | URL path segment (e.g., `/products`) |
| **Method** | HTTP verb assigned to a resource |
| **Integration** | Connects method to backend service (Lambda, HTTP, Mock, or AWS service) |
| **Stage** | Deployment environment (e.g., `dev`, `prod`) |
| **Endpoint Type** | Regional, Edge-Optimized, or Private |
| **API Key** | Optional authentication for client access |
| **Usage Plan** | Defines throttling, quota, and API key association |
| **Custom Domain** | Map API to your domain name |
| **Authorizers** | Implements authentication using **Cognito**, **Lambda**, or **IAM roles** |
| **Throttling & Quotas** | Control request rate and prevent overuse |

---

## 🌟 Use Cases

1. **Serverless Web Applications**
   - Frontend calls API Gateway → Lambda → DynamoDB

2. **Microservices Architecture**
   - Expose multiple microservices via a unified API

3. **Mobile or IoT Backend**
   - Provide REST APIs to mobile or IoT clients

4. **Real-Time Communication**
   - Use WebSocket APIs for chat apps, notifications, or IoT devices

5. **Third-Party API Monetization**
   - Apply API keys and usage plans for external developers

---

## 🧱 Best Practices

1. **Use Stages for Environment Management**
   - Separate `dev`, `test`, and `prod` APIs

2. **Enable Caching**
   - Reduce backend load and improve latency

3. **Secure APIs**
   - Use IAM roles, Cognito, or API keys

4. **Enable Logging and Metrics**
   - Monitor API usage and troubleshoot via CloudWatch

5. **Set Throttling and Quotas**
   - Protect backend services from overuse or abuse

6. **Use Private APIs**
   - For internal communication within VPCs

7. **Version APIs**
   - Avoid breaking client integrations

---

## 🧠 Practical Example: Serverless REST API

### Scenario:
Create an API to fetch user data using **API Gateway + Lambda + DynamoDB**.

### Steps:

1. **Create DynamoDB Table**
   - Table Name: `Users`
   - Partition Key: `UserId` (String)

2. **Create Lambda Function**
   - Language: Python
   - Function Name: `GetUser`
   - Fetches data from DynamoDB

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')

def lambda_handler(event, context):
    user_id = event['queryStringParameters']['id']
    response = table.get_item(Key={'UserId': user_id})
    return {
        'statusCode': 200,
        'body': json.dumps(response.get('Item', {}))
    }
````

3. **Create REST API**

   * Resource: `/users`
   * Method: `GET`
   * Integration: Lambda Function `GetUser`
   * Deployment Stage: `prod`

4. **Invoke API**

```bash
curl https://<api-id>.execute-api.<region>.amazonaws.com/prod/users?id=123
```

Output:

```json
{
  "UserId": "123",
  "Name": "John Doe",
  "Email": "john@example.com"
}
```

✅ You now have a **working serverless API** using Amazon API Gateway.

---

## 🧾 Conclusion

Amazon API Gateway is a **robust, fully managed API solution** that simplifies **API creation, deployment, security, and monitoring**.
It is ideal for **serverless architectures, microservices, mobile backends, and real-time applications**, offering scalability and secure integration with AWS services.

> **Key takeaway:** API Gateway = **Your scalable, secure, and monitored front door to backend services**.

---
