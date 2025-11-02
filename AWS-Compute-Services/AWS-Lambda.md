# ⚡ AWS Lambda

## 🌐 1. What is AWS Lambda?
**AWS Lambda** is a **serverless compute service** that automatically runs your code **without provisioning or managing servers**.  
You just upload your code — Lambda takes care of execution, scaling, and availability.  

> 💡 Think of it as “run your code only when needed” — AWS handles everything else!

---

## ⚙️ 2. How to Configure AWS Lambda

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

## ⚙️ 3. How Does It Work?
1. **Trigger/Event:**

   * Lambda is invoked automatically by an event (e.g., an S3 upload, API Gateway request, or CloudWatch event).

2. **Execution:**

   * AWS runs your function code in a secure, temporary container with allocated memory and CPU.

3. **Scaling:**

   * Lambda automatically creates more instances of the function if multiple events occur simultaneously.

4. **Completion:**

   * Once execution finishes, AWS shuts down the container. You’re charged only for the execution time.

👉 **In simple terms:**
**Event triggers function → AWS runs code → Scales automatically → Stops when done → Pay only for use.**


---

## 💡 4. Lambda Function
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

## 📦 5. Lambda Layers

**AWS Lambda Layer** is a feature that lets you **package and share reusable code, libraries, or dependencies** separately from your main function code.

👉 **In short:**
A **Layer** is like a **shared library** for Lambda — you can include things like SDKs, custom modules, or configuration files without bundling them into every function.

**Example:**
If multiple Lambda functions use the same Python library, you can put that library in a **Layer** and attach it to all functions — saving space and making updates easier.

> You can include **up to 5 layers** per function.

---

## 🔔 6. Lambda Events

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

## 🧩 7. Languages Supported

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

## 💰 8. Pricing

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

## 🧠 9. Practical Example: Auto File Sorter with AWS Lambda (PDF, JPG, TXT)

### **Description:**

This Lambda function is triggered **automatically when a new object is uploaded** to an S3 source bucket.
It checks the **file type (extension)** and **copies** it to a **specific destination bucket** based on its type:

* **PDF → pdf-bucket**
* **JPG → image-bucket**
* **TXT → text-bucket**

> AWS Lambda Function to Automatically copies Uploaded PDF, JPG, and TXT Files to Separate Buckets
---

### **Python Lambda Function Code (Python 3.9 or later)**

```python
import boto3
import os

s3 = boto3.client('s3')

def lambda_handler(event, context):
    # Extract bucket name and object key from the event
    source_bucket = event['Records'][0]['s3']['bucket']['name']
    object_key = event['Records'][0]['s3']['object']['key']
    
    # Extract file extension
    file_extension = os.path.splitext(object_key)
    file_extension = file_extension.lower()
    
    # Define destination buckets for each file type
    pdf_bucket = 'your-pdf-bucket-name'
    image_bucket = 'your-image-bucket-name'
    text_bucket = 'your-text-bucket-name'
    
    # Determine destination bucket based on file type
    if file_extension == '.pdf':
        destination_bucket = pdf_bucket
    elif file_extension in ['.jpg', '.jpeg']:
        destination_bucket = image_bucket
    elif file_extension == '.txt':
        destination_bucket = text_bucket
    else:
        print(f"Unsupported file type: {file_extension}")
        return
    
    # Copy file to destination bucket
    copy_source = {'Bucket': source_bucket, 'Key': object_key}
    s3.copy_object(CopySource=copy_source, Bucket=destination_bucket, Key=object_key)
    
    # Optional: delete the file from source after copying
    # s3.delete_object(Bucket=source_bucket, Key=object_key)
    
    print(f"File '{object_key}' moved from '{source_bucket}' to '{destination_bucket}'")

```

---

### **Setup Steps:**

1. **Create 4 S3 Buckets:**

   * `source-bucket` (upload files here)
   * `pdf-bucket`
   * `image-bucket`
   * `text-bucket`

2. **Create a Lambda Function:**

   * Runtime: **Python 3.9**
   * Role permissions:
     Add **S3FullAccess** (or fine-tuned policy for GetObject, PutObject, DeleteObject)

3. **Add S3 Trigger:**

   * Configure the Lambda trigger for your **source bucket**
   * Event type: **“All object create events”**
   * Filter suffixes (optional): `.pdf`, `.jpg`, `.txt`

4. **Deploy and Test:**

   * Upload a file (like `example.pdf`) to your source bucket
   * The Lambda will automatically copy it to the right destination bucket

---


## 🧠 10. Practical Example: Auto Thumbnail Generator

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
## ⚡ 11. **Advantages of AWS Lambda**

1. **No Server Management**

   * You don’t need to provision, configure, or maintain servers — AWS handles all infrastructure.

2. **Automatic Scaling**

   * Lambda automatically scales based on the number of incoming requests or events.

3. **Cost Efficiency (Pay-as-you-go)**

   * You only pay for the compute time consumed (measured in milliseconds), not for idle time.

4. **Event-Driven Execution**

   * Can be easily triggered by AWS services like S3, DynamoDB, SNS, API Gateway, CloudWatch, etc.

5. **Supports Multiple Languages**

   * Supports Node.js, Python, Java, Go, C#, Ruby, and custom runtimes via Lambda Runtime API.

6. **Quick Deployment**

   * Simple to upload and deploy code directly from the console or CLI without worrying about servers.

7. **Integrated Security**

   * Works seamlessly with AWS IAM for fine-grained access control.

8. **Built-in Fault Tolerance**

   * AWS Lambda runs functions across multiple Availability Zones automatically for high availability.

9. **Easily Connects with AWS Ecosystem**

   * Tight integration with AWS services makes it ideal for building serverless applications.

10. **Versioning and Aliases**

    * Allows maintaining different versions of functions and routing traffic between them.

---

## ⚠️ 12. **Limitations of AWS Lambda**

1. **Limited Execution Time**

   * Maximum execution timeout is **15 minutes** per function invocation.

2. **Cold Start Latency**

   * First invocation after a period of inactivity may experience a delay (especially for large packages or Java-based functions).

3. **Limited Temporary Storage**

   * `/tmp` directory provides only **512 MB** of ephemeral storage (though expandable up to 10 GB).

4. **Memory and CPU Constraints**

   * Memory can be configured between **128 MB and 10 GB**, with proportional CPU — not suitable for heavy compute tasks.

5. **Complex Debugging and Monitoring**

   * Harder to debug locally compared to traditional servers; relies on CloudWatch Logs.

6. **Vendor Lock-in**

   * Deep integration with AWS services can make migration to other platforms challenging.

7. **No Direct SSH Access**

   * You cannot log in to the runtime environment to inspect or troubleshoot directly.

8. **Concurrency Limits**

   * Each account has default concurrency limits (though can be increased via AWS Support).

9. **Deployment Package Size Limit**

   * The size of deployment packages (including dependencies) is limited — **50 MB (zipped)** or **250 MB (unzipped)**.

10. **Not Ideal for Long-Running Applications**

    * Workloads requiring continuous processing (like streaming or large batch jobs) are not suitable for Lambda.

---

## ✅ 13. Summary

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

--- 
