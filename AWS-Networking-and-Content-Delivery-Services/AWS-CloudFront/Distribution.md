

## What is a CloudFront Distribution?

An **Amazon CloudFront distribution** is a configuration that tells **CloudFront (AWS CDN)**:

* **Where your content is stored (Origin)**
* **How CloudFront should cache and deliver it**
* **Who can access it and how**

Once a distribution is created, CloudFront uses its **global Edge Locations** to serve content to users with **low latency and high performance**.

---

## Why Do We Need CloudFront Distribution?

Without CloudFront:

* Users access content directly from the origin (EC2, S3, ALB)
* Higher latency for global users
* More load on backend servers

With CloudFront:

* Content is cached at edge locations
* Faster response time
* Reduced backend load
* Built-in security (HTTPS, WAF, signed URLs)

---

## Key Components of a CloudFront Distribution

### 1️⃣ Origin

The **source of your content**

Supported origins:

* **S3 bucket** (static website, images)
* **EC2 instance**
* **Application Load Balancer**
* **Custom HTTP server**

Example:

```
Origin = S3 bucket (my-static-site)
```

---

### 2️⃣ Edge Locations

* Global AWS data centers
* Cache content close to users

User → Nearest Edge Location → (Origin only if cache miss)

---

### 3️⃣ Cache Behavior

Defines **how CloudFront handles requests**

Includes:

* Path pattern (`/images/*`)
* Allowed HTTP methods (GET, POST)
* TTL (Time to Live)
* Query string & cookie forwarding

Default behavior:

```
Path pattern: *
Allowed methods: GET, HEAD
TTL: 24 hours
```

---

### 4️⃣ Viewer Protocol Policy

Controls HTTP/HTTPS behavior

* Redirect HTTP to HTTPS
* HTTPS only
* HTTP & HTTPS

---

### 5️⃣ Domain Name

CloudFront provides:

```
d123abcd.cloudfront.net
```

You can map a custom domain:

```
www.example.com
```

---

### 6️⃣ Security Options

* HTTPS (SSL/TLS)
* AWS WAF
* Geo restriction
* Signed URLs / Signed Cookies

---

## CloudFront Distribution – Simple Example (S3 Static Website)

### Scenario

You have a **static website** stored in S3:

* HTML, CSS, JS, Images
* Users from India, US, Europe

---

### Step 1: Create S3 Bucket

```
Bucket name: my-static-website
Enable static website hosting
Upload index.html
```

---

### Step 2: Create CloudFront Distribution

| Setting             | Value                              |
| ------------------- | ---------------------------------- |
| Origin domain       | my-static-website.s3.amazonaws.com |
| Origin type         | S3                                 |
| Viewer protocol     | Redirect HTTP → HTTPS              |
| Cache policy        | CachingOptimized                   |
| Default root object | index.html                         |

---

### Step 3: Access Website

CloudFront URL:

```
https://d3xyzabc.cloudfront.net
```

User flow:

```
User (India)
   ↓
Nearest CloudFront Edge (Mumbai)
   ↓
Cached content returned
```

If cache miss:

```
Edge → S3 → Cache → User
```

---

## CloudFront Distribution – EC2 Example (Dynamic Website)

### Scenario

* Nginx running on EC2
* Public users accessing website
* Want caching + security

---

### Architecture

```
User → CloudFront → EC2 (Nginx)
```

---

### Distribution Settings

| Setting         | Value                                         |
| --------------- | --------------------------------------------- |
| Origin          | EC2 Public DNS                                |
| Origin protocol | HTTP                                          |
| Cache policy    | Managed-CachingDisabled (for dynamic content) |
| Allowed methods | GET, POST                                     |
| Security        | HTTPS + WAF                                   |

---

### Benefit

* DDoS protection
* SSL termination
* Faster content delivery
* Can restrict EC2 access to CloudFront only

---

## CloudFront with ALB (Production Setup)

```
Users → CloudFront → ALB → EC2 Auto Scaling
```

Advantages:

* High availability
* Auto scaling
* Central SSL management
* Backend not exposed publicly

---

## Cache TTL Example

| TTL Type    | Meaning                |
| ----------- | ---------------------- |
| Min TTL     | Minimum cache time     |
| Default TTL | Normal cache duration  |
| Max TTL     | Maximum cache duration |

Example:

```
Default TTL = 3600 seconds (1 hour)
```

---

## Common Use Cases

✔ Static websites
✔ Video streaming
✔ API acceleration
✔ Software downloads
✔ Secure private content

---

## CloudFront Distribution vs Direct Access

| Feature           | Without CloudFront | With CloudFront |
| ----------------- | ------------------ | --------------- |
| Latency           | High               | Low             |
| Global reach      | ❌                  | ✅               |
| Security          | Limited            | Strong          |
| Backend load      | High               | Low             |
| Cost optimization | ❌                  | ✅               |

---

## Interview One-Line Summary

> **A CloudFront distribution defines how CloudFront delivers content from an origin to users via global edge locations with caching, security, and performance optimization.**

---

