
## What is Amazon CloudFront?

**Amazon CloudFront** is a **Content Delivery Network (CDN)** service provided by AWS that **delivers content to users with low latency and high speed** by caching it at **edge locations** around the world.

👉 Instead of users accessing your server directly, they access the **nearest CloudFront edge location**.

---

## Why do we need CloudFront?

Problems without CloudFront:

* High latency for users far from the server
* Heavy load on origin server (EC2 / S3)
* Slow website performance
* Higher bandwidth cost

CloudFront solves:

* ⚡ Faster content delivery
* 🌍 Global reach
* 🔐 Better security
* 💰 Reduced origin load & cost

---

## How CloudFront Works (Simple Flow)

```
User → CloudFront Edge Location → Origin (EC2 / S3 / ALB)
```

### Step-by-step:

1. User requests a file (image, video, API)
2. CloudFront checks **nearest edge location**
3. If content exists in cache → served immediately
4. If not cached:

   * CloudFront fetches from **origin**
   * Stores it in cache
   * Serves to user

---

## Key CloudFront Components

### 1. Edge Locations

* Global data centers where content is cached
* Example: Mumbai, Singapore, Frankfurt, US-East

---

### 2. Origin

Source of content:

* S3 bucket
* EC2 instance
* Application Load Balancer
* API Gateway

---

### 3. Distribution

Configuration that connects:

* Edge locations
* Origin
* Cache behavior
* Security rules

---

### 4. Cache Behavior

Defines:

* Which HTTP methods allowed
* TTL (cache duration)
* Forward headers, cookies, query strings

---

### 5. TTL (Time To Live)

How long content stays cached:

* Min TTL
* Default TTL
* Max TTL

---

## CloudFront Supported Content Types

| Type      | Example               |
| --------- | --------------------- |
| Static    | HTML, CSS, JS, Images |
| Dynamic   | API responses         |
| Streaming | Video, Audio          |
| Secure    | Private content       |

---

## Example 1: CloudFront with S3 (Static Website)

### Scenario:

You host a static website on **S3**.

### Without CloudFront:

```
User (India) → S3 (us-east-1)
```

❌ High latency

### With CloudFront:

```
User (India) → CloudFront (Mumbai) → S3 (us-east-1)
```

✅ Faster loading

### Setup:

1. Create S3 bucket
2. Upload static files
3. Create CloudFront distribution
4. Set S3 as origin
5. Use CloudFront URL

### Result:

* Website loads faster globally
* Reduced S3 data transfer cost

---

## Example 2: CloudFront with EC2 (Dynamic Content)

### Scenario:

You deployed **Nginx on EC2** serving a website.

### Architecture:

```
User → CloudFront → EC2 (Nginx)
```

### Benefits:

* Caching static files
* Reduced EC2 CPU usage
* Improved response time

### Security Enhancement:

* Remove public access to EC2
* Allow only CloudFront using:

  * Security Group
  * Custom headers
  * AWS WAF

---

## Example 3: CloudFront for API Acceleration

### Scenario:

Backend API hosted on ALB.

### Architecture:

```
Client → CloudFront → ALB → EC2
```

### Benefits:

* Global API acceleration
* DDoS protection
* TLS termination

---

## CloudFront Security Features

### 1. HTTPS (SSL/TLS)

* Free SSL via AWS Certificate Manager

---

### 2. Origin Access Control (OAC)

* Prevents direct access to S3
* Only CloudFront can access bucket

---

### 3. AWS WAF

* Block IPs, bots, SQL injection, XSS

---

### 4. Signed URLs & Signed Cookies

* Restrict content access
* Used for paid or private content

---

## CloudFront vs ELB vs S3 (Quick Comparison)

| Feature        | CloudFront | ELB | S3 |
| -------------- | ---------- | --- | -- |
| Global         | ✅          | ❌   | ❌  |
| Caching        | ✅          | ❌   | ❌  |
| Load Balancing | ❌          | ✅   | ❌  |
| Storage        | ❌          | ❌   | ✅  |

---

## CloudFront Pricing

* Data transfer out
* HTTP/HTTPS requests
* Invalidation requests (after free limit)

💡 **Caching reduces cost significantly**

---

## Real-World Use Cases

✔ Static website hosting
✔ Video streaming platforms
✔ Secure API delivery
✔ Software downloads
✔ E-commerce websites

---

## Interview One-Line Answer

> **Amazon CloudFront is a CDN service that delivers content globally with low latency by caching data at edge locations closer to users.**

---
