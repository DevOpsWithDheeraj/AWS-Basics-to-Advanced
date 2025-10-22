# 🌐 Amazon API Gateway 

## 📘 What is Amazon API Gateway?

**Amazon API Gateway** is a **fully managed service** that enables developers to **create, publish, maintain, monitor, and secure APIs** at any scale.  
It acts as a **front door** for applications to access data, business logic, or functionality from backend services like **AWS Lambda, EC2, or any web application**.

Key capabilities:
- **Create REST, HTTP, and WebSocket APIs**
- **Throttle traffic** and enforce quotas
- **Monitor APIs** via CloudWatch
- **Secure APIs** with authentication, authorization, and encryption

> Simply put, API Gateway **connects clients to your backend services securely and reliably**.

---

## ⚙️ How to Configure Amazon API Gateway

### Step-by-Step Configuration

1. **Open API Gateway Console**
   - Navigate to **AWS Management Console → API Gateway → Create API**.

2. **Choose API Type**
   - **HTTP API**: Simplified, low-latency API
   - **REST API**: Full-featured API with advanced options
   - **WebSocket API**: Real-time communication

3. **Define API Settings**
   - API Name: `MyAppAPI`
   - Endpoint Type: `Regional`, `Edge-Optimized`, or `Private`

4. **Create Resources & Methods**
   - **Resource**: Path for API, e.g., `/users`
   - **Method**: HTTP verb, e.g., `GET`, `POST`, `PUT`, `DELETE`
   - Connect method to **backend integration** (Lambda, HTTP endpoint, or Mock)

5. **Configure Security**
   - Enable **IAM roles**, **Cognito user pools**, or **API keys**
   - Set **throttling and quotas** if required

6. **Deploy API**
   - Create a **Stage**, e.g., `dev`, `test`, `prod`
   - Obtain **invoke URL** for client access

7. **Monitor**
   - Use **CloudWatch metrics and logs** to track API usage, latency, and errors

---

## 🧩 Components of API Gateway

| Component | Description |
|------------|--------------|
| **API** | The container for all resources and methods. |
| **Resource** | URL path segment, e.g., `/products`, `/orders`. |
| **Method** | HTTP verb for a resource, e.g., GET, POST, DELETE. |
| **Integration** | Connects the method to backend service (Lambda, HTTP endpoint, Mock, or AWS service). |
| **Stage** | Deployment environment for API (`dev`, `prod`). |
| **Endpoint Type** | Determines API access: Regional, Edge-Optimized, Private. |
| **API Key** | Optional authentication mechanism for usage plans. |
| **Usage Plan** | Define throttling, quota, and API key association. |
| **Custom Domain** | Map API to your own domain name. |
| **Throttling & Quotas** | Control request rate and prevent overuse. |
| **Authorizers** | Implement authentication using **Cognito**, **Lambda**, or **IAM roles**. |

---

## 🔗 Endpoint Types

1. **Regional**
   - API hosted in a single region
   - Low latency for region-specific traffic

2. **Edge-Optimized**
   - Uses **Amazon CloudFront** for global access
   - Ideal for APIs serving clients worldwide

3. **Private**
   - Accessible only from **VPC via VPC Endpoint**
   - Ensures private connectivity without internet exposure

---

## 🌉 VPC Integration

- **Private API Gateway** can be accessed through **VPC Endpoint (Interface type)**.
- Useful for internal APIs within a private network.
- Unlike VPC Peering (used for VPC-to-VPC communication), API Gateway private endpoints allow **direct access to your API from VPC securely**.

---

## 🌟 Use Cases

1. **Serverless Web Applications**
   - Frontend calls API Gateway → Lambda → DynamoDB
2. **Microservices Architecture**
   - Expose multiple microservices through a unified API
3. **Real-time Communication**
   - Use WebSocket API for chat applications or IoT devices
4. **Mobile/IoT Backend**
   - Provide RESTful APIs to mobile or IoT clients
5. **Third-Party API Monetization**
   - Apply usage plans and API keys for external developers

---

## 🧱 Best Practices

1. **Use Stages for Environment Management**
   - Separate `dev`, `test`, and `prod` APIs
2. **Enable Caching**
   - Reduce backend load and improve performance
3. **Secure APIs**
   - Use **IAM roles, Cognito, or API keys**
4. **Enable Logging and Metrics**
   - CloudWatch integration for monitoring and debugging
5. **Set Throttling & Quotas**
   - Protect backend from spikes or abuse
6. **Use Private Endpoints**
   - Keep internal APIs isolated from public internet
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
   - Reads data from DynamoDB

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
   * Integration: Lambda Function (`GetUser`)
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

✅ You now have a **fully working serverless API** using Amazon API Gateway.

---

## 🧾 Conclusion

Amazon API Gateway is a **robust and fully managed solution** to expose APIs to clients securely and reliably.
It simplifies API management, supports **serverless architectures**, and provides **monitoring, throttling, and authentication** out-of-the-box.

> **Key takeaway:** API Gateway = **Your front door to backend services**, scalable, secure, and ready for production workloads.

---
