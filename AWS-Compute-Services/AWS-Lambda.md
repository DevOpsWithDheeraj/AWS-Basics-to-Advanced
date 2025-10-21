# ⚡ AWS Lambda

## 🌐 What is AWS Lambda?
**AWS Lambda** is a **serverless compute service** that automatically runs your code **without provisioning or managing servers**.  
You just upload your code — Lambda takes care of execution, scaling, and availability.  

> 💡 Think of it as “run your code only when needed” — AWS handles everything else!

---

## ⚙️ How to Configure AWS Lambda

1. **Open AWS Console** → Go to **AWS Lambda** service.  
2. Click **Create Function** → Choose:
   - **Author from scratch**  
   - **Container image** (from ECR)  
   - **Blueprint** (predefined template)
3. Enter Function name → e.g., `MyFirstLambda`
4. Choose Runtime (e.g., Python 3.9, Node.js 18.x)
5. Choose or create an **Execution Role (IAM Role)** with Lambda permissions.
6. Add code (inline editor or upload `.zip` file / S3).
7. Configure a **Trigger** (like API Gateway, S3, DynamoDB, etc.)
8. Set **Memory**, **Timeout**, and **Environment Variables**.
9. Click **Deploy** → then **Test** your Lambda function.

---

## ⚙️ How Does It Work?
1. **Trigger/Event Source** (like S3 upload, API call, or scheduled CloudWatch event) invokes Lambda.
2. **Lambda receives the event**, executes your function code in an isolated container.
3. **Scales automatically** — Lambda launches as many parallel instances as needed.
4. **Stops automatically** when execution completes — you pay only for compute time.

---

## 💡 Lambda Function
A **Lambda Function** is the core component — your executable code plus configuration.  
Each function includes:
- **Handler** → Entry point of execution.  
- **Runtime** → Programming language environment.  
- **Memory & Timeout Settings**.  
- **Triggers** → Sources that invoke the function.  
- **Execution Role** → Defines AWS permissions.

Example (Python):
```python
def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello from AWS Lambda!'
    }
````

---

## 📦 Lambda Layers

**Lambda Layers** are reusable packages of code or dependencies (e.g., libraries, SDKs).
They help reduce code duplication across multiple Lambda functions.

Example use cases:

* Common logging library shared by multiple functions.
* Machine Learning models or Python packages.

You can include **up to 5 layers** per function.

---

## 🔔 Lambda Events

Lambda functions are triggered by **events** — objects that describe what happened.

| Event Source        | Example Use Case              |
| ------------------- | ----------------------------- |
| **API Gateway**     | Run Lambda when API is called |
| **S3 Bucket**       | Process image/file upload     |
| **DynamoDB Stream** | Process DB changes            |
| **SNS/SQS**         | Process messages              |
| **EventBridge**     | Respond to system events      |
| **CloudWatch**      | Run on a schedule (cron)      |

Example S3 Event (JSON):

```json
{
  "Records": [
    {
      "s3": {
        "bucket": { "name": "mybucket" },
        "object": { "key": "photo.jpg" }
      }
    }
  ]
}
```

---

## 🧩 Languages Supported

AWS Lambda supports multiple runtimes:

| Language | Runtime                                       |
| -------- | --------------------------------------------- |
| Node.js  | nodejs18.x, nodejs20.x                        |
| Python   | python3.8, python3.9, python3.12              |
| Java     | java11, java17                                |
| Go       | go1.x                                         |
| Ruby     | ruby3.2                                       |
| .NET     | dotnet8                                       |
| Custom   | Container or Custom Runtime (via Runtime API) |

---

## 💰 Pricing

AWS Lambda charges are based on **compute time and requests**:

| Factor                      | Description                               |
| --------------------------- | ----------------------------------------- |
| **Requests**                | First 1 million requests/month are free   |
| **Duration**                | Charged per millisecond of execution time |
| **Memory**                  | You choose 128 MB – 10 GB                 |
| **Compute Charges**         | Based on GB-seconds used                  |
| **Provisioned Concurrency** | Extra cost for pre-warmed Lambdas         |

> 💡 **Free Tier:** 1M requests + 400,000 GB-seconds per month!

---

## 🧠 Practical Example: Auto Thumbnail Generator

### Scenario:

When a user uploads a photo to **S3**, Lambda automatically creates a **thumbnail image**.

### Steps:

1. **Create S3 Bucket**

   * Bucket name: `my-photo-upload`
   * Enable event notifications for `PUT` object.
2. **Create Lambda Function**

   * Name: `ThumbnailGenerator`
   * Runtime: Python 3.9
   * Permissions: Allow read/write to S3
3. **Code Example:**

   ```python
   import boto3
   from PIL import Image
   import io

   s3 = boto3.client('s3')

   def lambda_handler(event, context):
       bucket = event['Records'][0]['s3']['bucket']['name']
       key = event['Records'][0]['s3']['object']['key']
       
       # Get the uploaded image
       img_obj = s3.get_object(Bucket=bucket, Key=key)
       image = Image.open(img_obj['Body'])
       
       # Create thumbnail
       image.thumbnail((100, 100))
       buffer = io.BytesIO()
       image.save(buffer, 'JPEG')
       buffer.seek(0)

       # Upload to thumbnails folder
       s3.put_object(Bucket=bucket, Key=f"thumbnails/{key}", Body=buffer)
       return f"Thumbnail created for {key}"
   ```
4. **Trigger:**

   * Event Source: S3 (ObjectCreated:Put)
5. **Test:**

   * Upload an image → Lambda runs → Thumbnail saved in `thumbnails/` folder.

🎉 Result: Fully automated, serverless image processing system!

---

## ✅ Summary

| Component          | Description                                              |
| ------------------ | -------------------------------------------------------- |
| **Lambda**         | Serverless compute service                               |
| **Function**       | Code + configuration                                     |
| **Layer**          | Shared dependencies/libraries                            |
| **Event**          | Trigger that invokes function                            |
| **Languages**      | Python, Node.js, Java, Go, etc.                          |
| **Pricing**        | Pay per request & execution time                         |
| **Scaling**        | Auto and infinite scaling                                |
| **Best Use Cases** | API backends, automation, data processing, file handling |

---

### 💡 Tip:

Combine **Lambda + API Gateway + DynamoDB** to build a **completely serverless web application** — scalable, cost-efficient, and maintenance-free!

```
