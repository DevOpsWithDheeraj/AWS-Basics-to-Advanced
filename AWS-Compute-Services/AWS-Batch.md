# 🗂️ AWS Batch

## 🌐 What is AWS Batch?
**AWS Batch** is a **fully managed batch computing service** that allows you to efficiently run **batch jobs** on AWS.  
It automatically provisions the right amount and type of compute resources (e.g., EC2 instances or Spot Instances) based on the volume and requirements of your jobs.  

> 💡 Think of it as “job scheduler + auto-scaling compute cluster” in the cloud.

---

## ⚙️ How AWS Batch Works
1. **Define a Job** → Specify the application or script you want to run.  
2. **Create a Job Definition** → Container image, vCPU, memory, environment variables, IAM role.  
3. **Submit Job to Job Queue** → Jobs wait in the queue until resources are available.  
4. **AWS Batch Scheduler** → Picks jobs from the queue and launches them on the appropriate compute environment.  
5. **Auto Scaling** → Batch automatically provisions and scales EC2 instances as needed.  

---

## ⚙️ How to Configure AWS Batch

### Step 1️⃣ – Create a Compute Environment
- Go to **AWS Batch Console → Compute environments → Create**  
- Select:
  - Managed or Unmanaged
  - EC2 or Spot instances
  - Instance types (e.g., `t3.medium`, `m5.large`)
  - Min, Max, Desired vCPUs
- Attach an IAM role (to allow EC2 instances to access S3, logs, etc.)

### Step 2️⃣ – Create a Job Queue
- Go to **Job Queues → Create Job Queue**
- Assign a **priority**  
- Attach the **compute environment** created in Step 1

### Step 3️⃣ – Create a Job Definition
- Go to **Job Definitions → Create**
- Specify:
  - Container image (ECR/Docker Hub)
  - vCPU and memory
  - Environment variables
  - Retry strategy, timeout
  - IAM role for job execution

### Step 4️⃣ – Submit Jobs
- Go to **Jobs → Submit Job**
- Choose:
  - Job name
  - Job definition
  - Job queue
  - Parameters (if needed)

AWS Batch will schedule and run jobs automatically.

---

## 🧩 Key Components of AWS Batch

| Component | Description |
|------------|-------------|
| **Job Definition** | Template for jobs (container, resources, env variables) |
| **Job Queue** | Queue that holds submitted jobs |
| **Compute Environment** | EC2 or Spot instances where jobs run |
| **Scheduler** | Decides which jobs run and when |
| **Job** | Individual task submitted to Batch |

---

## 💰 Pricing
- **No additional AWS Batch charges** — you pay only for underlying resources:
  - EC2 instances or Spot instances
  - EBS volumes or ephemeral storage
- Example: Running a job on `t3.medium` for 2 hours will incur EC2 cost for that duration.

---

## 🧠 Practical Example: Image Processing Batch Job

### Scenario:
Process a **large batch of images** uploaded to S3 — resize them to thumbnails using AWS Batch.

---

### Step 1️⃣ – Containerize the App
**Python Script (`resize.py`)**
```python
from PIL import Image
import boto3
import os

s3 = boto3.client('s3')
bucket_name = os.environ['BUCKET_NAME']

def resize_image(file_key):
    s3.download_file(bucket_name, file_key, '/tmp/input.jpg')
    img = Image.open('/tmp/input.jpg')
    img.thumbnail((100,100))
    img.save('/tmp/output.jpg')
    s3.upload_file('/tmp/output.jpg', bucket_name, f'thumbnails/{file_key}')

if __name__ == "__main__":
    import sys
    file_key = sys.argv[1]
    resize_image(file_key)
````

**Dockerfile**

```dockerfile
FROM python:3.9
WORKDIR /app
COPY resize.py .
RUN pip install boto3 pillow
CMD ["python", "resize.py"]
```

Build and push image to **Amazon ECR**:

```bash
docker build -t batch-image-resizer .
docker tag batch-image-resizer:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/batch-image-resizer:latest
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/batch-image-resizer:latest
```

---

### Step 2️⃣ – Configure AWS Batch

1. **Compute Environment**:

   * Managed, EC2
   * Instance type: `t3.medium`
   * Min vCPU: 0, Max vCPU: 4
   * Spot instances allowed

2. **Job Queue**:

   * Name: `ImageProcessingQueue`
   * Priority: 1
   * Linked Compute Environment: Above

3. **Job Definition**:

   * Container image: `<ECR URL>`
   * vCPU: 1
   * Memory: 2 GB
   * Environment variable: `BUCKET_NAME=my-image-bucket`
   * Retry strategy: 2 retries

---

### Step 3️⃣ – Submit Jobs

```bash
aws batch submit-job \
    --job-name resize-image-1 \
    --job-queue ImageProcessingQueue \
    --job-definition batch-image-resizer \
    --container-overrides command=["image1.jpg"]
```

* Repeat for multiple images. Batch scheduler will run them automatically.
* Output thumbnails appear in `thumbnails/` folder in S3.

---

## ✅ Summary

| Feature                 | Description                                                      |
| ----------------------- | ---------------------------------------------------------------- |
| **AWS Batch**           | Fully managed batch processing service                           |
| **Compute Environment** | Where jobs run (EC2/Spot instances)                              |
| **Job Queue**           | Queue to hold pending jobs                                       |
| **Job Definition**      | Template specifying container and resources                      |
| **Scheduler**           | Launches jobs automatically based on resources                   |
| **Pricing**             | Pay only for EC2, Spot, and storage used                         |
| **Use Cases**           | Large-scale data processing, ML training, media transcoding, ETL |

---

### 💡 Tip:

Use **Spot Instances in AWS Batch** to reduce costs for large-scale batch jobs while maintaining automatic scaling.

---
