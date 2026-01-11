

## 1️⃣ What is CloudFront Path-Based Routing?

**Path-based routing in CloudFront** means:

> CloudFront routes requests to **different origins** based on the **URL path** (e.g., `/images/*`, `/api/*`, `/videos/*`).

This is done using **Cache Behaviors**.

---

## 2️⃣ What is Multiple Origin in CloudFront?

A **CloudFront distribution** can have:

* **One default origin**
* **Multiple additional origins**

Each origin can be:

* S3 bucket
* EC2 / ALB / NLB
* API Gateway
* Media server
* Any HTTP server

CloudFront decides **which origin to use** based on the **request path**.

---

## 3️⃣ How CloudFront Decides Routing

CloudFront uses **Cache Behaviors** in this order:

1. **Exact path match** (e.g., `/api/login`)
2. **Longest path match** (e.g., `/api/*` before `/*`)
3. **Default behavior** (`/*`)

---

## 4️⃣ Architecture Example (Real World)

### Scenario

You have a web application with:

| Path        | Content      | Origin      |
| ----------- | ------------ | ----------- |
| `/`         | Web UI       | EC2 (Nginx) |
| `/images/*` | Images       | S3          |
| `/videos/*` | Videos       | S3          |
| `/api/*`    | Backend APIs | ALB (EC2)   |

---

### Architecture Diagram (Textual)

```
User
 │
 ▼
CloudFront (Single Distribution)
 │
 ├── /images/* ───▶ S3 Bucket (Images)
 ├── /videos/* ───▶ S3 Bucket (Videos)
 ├── /api/* ──────▶ ALB → EC2 (API)
 └── /* ──────────▶ EC2 (Nginx Web App)
```

---

## 5️⃣ Step-by-Step CloudFront Configuration

### Step 1: Create Origins

Create **multiple origins**:

1. **Origin 1**

   * Name: `web-ec2-origin`
   * Type: EC2 / ALB
   * Domain: `ec2-public-dns.amazonaws.com`

2. **Origin 2**

   * Name: `images-s3-origin`
   * Type: S3
   * Domain: `images-bucket.s3.amazonaws.com`

3. **Origin 3**

   * Name: `videos-s3-origin`
   * Type: S3
   * Domain: `videos-bucket.s3.amazonaws.com`

4. **Origin 4**

   * Name: `api-alb-origin`
   * Type: ALB
   * Domain: `api-alb.amazonaws.com`

---

### Step 2: Default Cache Behavior (`/*`)

| Setting                | Value                 |
| ---------------------- | --------------------- |
| Path Pattern           | `/*`                  |
| Origin                 | `web-ec2-origin`      |
| Viewer Protocol Policy | Redirect HTTP → HTTPS |
| Cache                  | Enabled               |

➡ Used for **UI pages**

---

### Step 3: Create Path-Based Cache Behaviors

#### `/images/*`

| Setting      | Value                |
| ------------ | -------------------- |
| Path Pattern | `/images/*`          |
| Origin       | `images-s3-origin`   |
| Cache        | Enabled              |
| TTL          | High (1 day or more) |

---

#### `/videos/*`

| Setting      | Value              |
| ------------ | ------------------ |
| Path Pattern | `/videos/*`        |
| Origin       | `videos-s3-origin` |
| Cache        | Enabled            |
| Compression  | Enabled            |

---

#### `/api/*`

| Setting         | Value                  |
| --------------- | ---------------------- |
| Path Pattern    | `/api/*`               |
| Origin          | `api-alb-origin`       |
| Cache           | Disabled               |
| Allowed Methods | GET, POST, PUT, DELETE |
| TTL             | 0                      |

---

## 6️⃣ Request Flow Example

### Example URL Requests

| Request URL                                   | Routed To        |
| --------------------------------------------- | ---------------- |
| `https://d123.cloudfront.net/`                | EC2 Web Server   |
| `https://d123.cloudfront.net/images/logo.png` | S3 Images Bucket |
| `https://d123.cloudfront.net/videos/demo.mp4` | S3 Videos Bucket |
| `https://d123.cloudfront.net/api/login`       | ALB → EC2 API    |

---

## 7️⃣ Why Use Path-Based Routing with CloudFront?

### ✅ Key Benefits

1. **Single Domain Name**

   ```
   https://example.com
   ```

   Instead of:

   ```
   api.example.com
   images.example.com
   ```

2. **Better Performance**

   * Static content cached at edge locations
   * Reduced load on backend servers

3. **Cost Optimization**

   * Fewer EC2/API calls
   * Cached S3 content

4. **Security**

   * Private S3 access via OAC
   * ALB protected by security group
   * AWS WAF integration

5. **Scalability**

   * Different services scale independently

---

## 8️⃣ Interview-Ready One-Line Explanation

> **CloudFront path-based routing allows a single distribution to route traffic to multiple origins based on URL paths using cache behaviors, enabling optimized performance, cost efficiency, and clean architecture.**

---

## 9️⃣ Common Interview Follow-Up Questions

**Q1. Can CloudFront route based on headers or query strings?**
✅ Yes, using cache behavior settings.

**Q2. Can two behaviors point to same origin?**
✅ Yes.

**Q3. Can CloudFront replace API Gateway?**
❌ No, but it can sit **in front of API Gateway**.

---
