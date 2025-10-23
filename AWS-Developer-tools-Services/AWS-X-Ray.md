# AWS X-Ray

## What is AWS X-Ray?

**AWS X-Ray** is a fully managed **distributed tracing service** that helps developers analyze and debug **production applications** built using microservices, serverless, or monolithic architectures.  

X-Ray enables you to **trace requests** as they travel through your application, visualize application components, identify performance bottlenecks, detect errors, and troubleshoot issues in real time.

---

## Key Features of AWS X-Ray

1. **End-to-End Request Tracing**: Track requests across multiple services, APIs, and resources.
2. **Service Maps**: Visual representation of your application architecture and interactions.
3. **Latency Analysis**: Detect performance bottlenecks in microservices or serverless functions.
4. **Error and Fault Detection**: Identify failing requests and exceptions.
5. **Integration**:
   - AWS Lambda
   - Amazon API Gateway
   - Elastic Load Balancer
   - Amazon EC2, ECS, EKS
   - Third-party applications (via X-Ray SDK)
6. **Sampling**: Control trace collection to reduce overhead.
7. **Annotations and Metadata**: Add custom key-value pairs to traces for filtering and debugging.
8. **Segmentation**: Break down requests into **segments** representing services or components.

---

## AWS X-Ray Architecture

1. **Client Request**: User sends a request to the application.
2. **Application Instrumentation**: X-Ray SDK collects **segments** and **subsegments** from the application.
3. **X-Ray Daemon**: Runs on EC2, ECS, or Lambda, and sends trace data to X-Ray service.
4. **X-Ray Service**: Aggregates and stores traces, generates service maps, and provides analytics.
5. **Service Map & Trace Data**:
   - Visualizes latency, errors, and request paths
   - Allows drill-down to specific traces

**Flow**:

```

Client → API Gateway / ELB → Service1 → Service2 → Database
|                 |         |
Trace Data → X-Ray SDK → X-Ray Daemon → X-Ray Service → Service Map & Analytics

````

---

## Step-by-Step Guide to Configure AWS X-Ray

### Step 1: Create IAM Role

1. Create **IAM Role** for application to send trace data:
   - Managed Policy: `AWSXRayDaemonWriteAccess`
2. For EC2:
   - Attach role to instance profile
3. For Lambda:
   - Add execution role permissions for X-Ray

---

### Step 2: Install X-Ray Daemon (For EC2/ECS)

**EC2 Amazon Linux 2 example**:

```bash
curl https://s3.us-east-1.amazonaws.com/aws-xray-assets.us-east-1/xray-daemon/aws-xray-daemon-linux-2.x.zip -o xray.zip
unzip xray.zip -d xray
sudo ./xray/xray -o
````

* Daemon listens on UDP port 2000 for trace data from the SDK.
* For ECS: Use **X-Ray sidecar container**.

---

### Step 3: Instrument Application with X-Ray SDK

#### Python Example

```python
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.core import patch_all

patch_all()  # Automatically instruments supported libraries

xray_recorder.configure(service='MyAppService')

from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello AWS X-Ray!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

#### Node.js Example

```javascript
const AWSXRay = require('aws-xray-sdk');
const express = require('express');

AWSXRay.captureHTTPsGlobal(require('http'));
const app = express();
app.use(AWSXRay.express.openSegment('MyAppService'));

app.get('/', (req, res) => {
    res.send('Hello AWS X-Ray!');
});

app.use(AWSXRay.express.closeSegment());
app.listen(3000, () => console.log('Server running'));
```

---

### Step 4: Enable X-Ray for Lambda

1. Go to Lambda function → Configuration → Monitoring and Operations → **Enable Active Tracing**
2. Lambda automatically sends traces to X-Ray.

---

### Step 5: Generate Sample Traffic

* Send requests to the instrumented application (EC2, ECS, or Lambda) to generate trace data.
* Example:

```bash
curl http://<EC2-PUBLIC-IP>:5000/
```

---

### Step 6: View Traces and Service Map

1. Go to **AWS Console → X-Ray → Service Map**
2. Visualize request flows, latency, errors, and dependencies.
3. Drill down into individual traces to see:

   * Segments (services/components)
   * Subsegments (database, API calls)
   * Latency, error, and exception data
4. Use **Filter Expressions** to find specific traces:

   * `response.status >= 400` → view failed requests
   * `annotation.UserId = 123` → filter by custom annotation

---

## Practical Example: Trace a Python Flask Microservice

### Scenario

* Flask app deployed on EC2, with a PostgreSQL database.
* Goal: Trace requests and database queries using X-Ray.

### Step 1: IAM Role

* Role: `EC2XRayRole`
* Policy: `AWSXRayDaemonWriteAccess`
* Attach to EC2 instance running Flask app.

### Step 2: Install X-Ray Daemon

```bash
wget https://s3.us-east-1.amazonaws.com/aws-xray-assets.us-east-1/xray-daemon/aws-xray-daemon-linux-2.x.zip
unzip aws-xray-daemon-linux-2.x.zip
sudo ./xray -o
```

### Step 3: Instrument Flask App

```python
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.core import patch_all
import psycopg2
from flask import Flask

patch_all()  # Automatically instruments supported libraries
xray_recorder.configure(service='FlaskApp')

app = Flask(__name__)

@app.route('/')
def hello():
    conn = psycopg2.connect("dbname=test user=postgres password=secret")
    cur = conn.cursor()
    cur.execute("SELECT NOW()")
    result = cur.fetchone()
    cur.close()
    conn.close()
    return f"Hello! DB time is {result[0]}"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### Step 4: Generate Traffic

```bash
curl http://<EC2-PUBLIC-IP>:5000/
```

### Step 5: View Traces

* Go to X-Ray Console → Service Map
* See:

  * Flask service → PostgreSQL database
  * Latency metrics
  * Any errors or exceptions

---

## Best Practices

1. **Use Sampling** to reduce overhead and cost.
2. **Add Annotations & Metadata** for easier trace filtering.
3. Monitor X-Ray in **production and staging** environments.
4. Enable **integration with CloudWatch** for alerts on latency and errors.
5. Use **service maps** to identify bottlenecks and optimize application performance.
6. Instrument all layers of application (API, DB, external services) for full visibility.

---

## Summary

AWS X-Ray provides **end-to-end observability** of distributed applications. It helps developers trace requests, analyze performance, identify errors, and optimize microservices or serverless architectures.

**Practical Example**: Python Flask app with PostgreSQL database traces requests, visualizes service map, and provides detailed latency and error analysis using AWS X-Ray.

---

**References**:

* [AWS X-Ray Documentation](https://docs.aws.amazon.com/xray/)
* [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)
