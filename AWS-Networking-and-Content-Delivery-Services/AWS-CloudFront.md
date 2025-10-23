# Amazon CloudFront

## What is Amazon CloudFront?

Amazon CloudFront is a **Content Delivery Network (CDN)** service offered by AWS. It delivers data, videos, applications, and APIs to customers globally with **low latency and high transfer speeds**. CloudFront caches content at **edge locations** worldwide, which ensures faster delivery by serving content from locations closest to end-users.

CloudFront integrates seamlessly with other AWS services like **S3, EC2, Lambda@Edge, and API Gateway**. It supports **dynamic and static content delivery**, and provides **security features** like SSL/TLS encryption and AWS Shield protection.

---

## Key Features of CloudFront

1. **Global Distribution**: Uses a network of **edge locations** to deliver content closer to users.
2. **Low Latency & High Throughput**: Reduces load time for websites and applications.
3. **Caching & TTL**: Supports caching of static and dynamic content; configurable **Time-to-Live (TTL)**.
4. **Security Integration**:
   - SSL/TLS encryption.
   - AWS WAF integration for application-level protection.
   - Signed URLs and cookies for private content access.
5. **Origin Flexibility**:
   - Supports **S3 buckets**, **EC2 instances**, **load balancers**, or **custom origins**.
6. **Real-Time Metrics**: Provides real-time monitoring via **CloudWatch**.
7. **Lambda@Edge**: Allows running serverless code at edge locations for request/response customization.

---

## CloudFront Architecture

1. **Origin**: The source of the content (S3, EC2, ALB, API Gateway, etc.).
2. **Edge Location**: Global points of presence where content is cached.
3. **Distribution**: A setup that tells CloudFront:
   - Which origin to fetch content from.
   - How to cache and serve content.
4. **Viewer**: End-users accessing your content via web browsers or apps.

**Flow**:
1. User requests content from CloudFront URL.
2. CloudFront checks cache in the nearest edge location.
3. If cached, content is served immediately.
4. If not, CloudFront fetches content from the origin, caches it, and serves it to the user.

---

## CloudFront Distribution Types

1. **Web Distribution**: For websites, APIs, and HTTP/HTTPS content.
2. **RTMP Distribution**: For streaming media using Adobe Flash (legacy, less common).

---

## Step-by-Step Guide to Configure CloudFront

### Step 1: Create a CloudFront Distribution

1. Go to **AWS Management Console** → **CloudFront** → **Create Distribution**.
2. Select **Web** distribution.
3. Configure the **origin settings**:
   - **Origin Domain Name**: Select your S3 bucket, EC2, ALB, or custom server.
   - **Origin Path**: Optional path prefix if you want CloudFront to serve content from a subdirectory.
   - **Origin ID**: A unique name for the origin.

### Step 2: Configure Default Cache Behavior

1. **Viewer Protocol Policy**: Redirect HTTP to HTTPS for security.
2. **Allowed HTTP Methods**: GET, HEAD (for static content); GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE for dynamic APIs.
3. **Cache Based on Query String**: Enable if your content varies based on query strings.
4. **Forward Headers/Cookies**: Configure if content varies for users or sessions.

### Step 3: Configure Distribution Settings

1. **Price Class**: Choose which edge locations you want to serve from (all locations or selected continents).
2. **Alternate Domain Names (CNAMEs)**: Add your domain name if you want CloudFront to serve via your custom domain.
3. **SSL Certificate**: Use **AWS Certificate Manager (ACM)** for HTTPS.
4. **Logging**: Enable access logging to S3 bucket for analytics.
5. **Default Root Object**: Example: `index.html` for website hosting.

### Step 4: Deploy the Distribution

1. Click **Create Distribution**.
2. CloudFront will take some time (~15–20 minutes) to deploy.
3. Once deployed, note the **CloudFront domain name** (`xxxx.cloudfront.net`).

### Step 5: Test the Distribution

1. Open the CloudFront URL in a browser.
2. Verify content loads correctly and caching works.
3. You can also use tools like `curl -I` to check response headers like `X-Cache: Hit from cloudfront`.

---

## Practical Example: Serving a Static Website from S3

### Step 1: Create S3 Bucket

1. Create a bucket named `my-website-bucket`.
2. Upload your `index.html` and other static files.
3. Enable **Static Website Hosting** on the S3 bucket.

### Step 2: Create CloudFront Distribution

- Origin: `my-website-bucket.s3.amazonaws.com`
- Viewer Protocol Policy: Redirect HTTP to HTTPS
- Cache Policy: Use **CachingOptimized** or create custom

### Step 3: Configure Custom Domain (Optional)

- Add `www.example.com` as **Alternate Domain Name (CNAME)**.
- Attach SSL certificate from **ACM**.

### Step 4: Update DNS

- Go to **Route 53** (or other DNS provider)
- Add **CNAME record** pointing `www.example.com` to `xxxx.cloudfront.net`.

### Step 5: Verify

- Access `https://www.example.com` → The site loads via CloudFront.
- Check headers: `X-Cache: Miss from cloudfront` (first time) and `X-Cache: Hit from cloudfront` (subsequent times).

---

## CloudFront Best Practices

1. Use **Lambda@Edge** for advanced request/response manipulation.
2. Enable **Gzip or Brotli compression** for faster content delivery.
3. Use **signed URLs or cookies** for private content.
4. Set appropriate **TTL values** to balance freshness vs. cache hits.
5. Enable **monitoring** via CloudWatch and **alerts** for operational issues.

---

## Summary

Amazon CloudFront is a powerful, globally distributed CDN service that accelerates content delivery, improves website performance, and enhances security. By integrating with other AWS services, CloudFront provides a flexible and scalable solution for static, dynamic, and streaming content.  

**Practical Example**: Hosting a static website on S3 and delivering it via CloudFront improves performance, adds HTTPS security, and can be customized via caching and Lambda@Edge.

---

**References**:

- [Amazon CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/)
- [AWS CDN Overview](https://aws.amazon.com/cloudfront/)
