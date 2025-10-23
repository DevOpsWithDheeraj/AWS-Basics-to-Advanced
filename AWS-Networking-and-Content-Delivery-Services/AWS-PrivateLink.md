# AWS PrivateLink

## What is AWS PrivateLink?

**AWS PrivateLink** is a service that provides **private connectivity** between VPCs, AWS services, and on-premises networks without exposing traffic to the public internet. It allows you to **securely access services** hosted on AWS over private IP addresses in your VPC.

PrivateLink uses **Elastic Network Interfaces (ENIs)** with private IPs in your VPC to connect to supported services. This is ideal for sensitive applications requiring high security and reduced exposure to the public internet.

---

## Key Features of AWS PrivateLink

1. **Private Connectivity**: Routes traffic over private IP addresses in your VPC.
2. **Secure Communication**: Avoids public internet; reduces attack surface.
3. **Service Consumer & Provider Model**:
   - **Service Provider**: Offers a service in their VPC.
   - **Service Consumer**: Connects privately to the provider’s service.
4. **Simplified Network Architecture**: No need for VPN, NAT, or public IPs.
5. **Supports Many AWS Services**: EC2, ALB, NLB, S3, API Gateway, and Marketplace services.
6. **Highly Scalable & Managed**: AWS handles scaling and availability.
7. **Cross-VPC & Cross-Account Access**: Services can be shared across accounts securely.

---

## AWS PrivateLink Architecture

1. **Service Provider**: Creates a **Network Load Balancer (NLB)** to expose the service privately.
2. **VPC Endpoint Service**: Provider registers NLB as an endpoint service in PrivateLink.
3. **Service Consumer**: Creates a **VPC Endpoint** in their VPC and connects to the provider’s endpoint service.
4. **Elastic Network Interface (ENI)**: Private IP in consumer’s VPC that acts as an entry point to the provider service.
5. **Traffic Flow**:
   - Consumer → VPC Endpoint → ENI → NLB → Service
   - Entire traffic remains within AWS private network.

---

## Step-by-Step Guide to Configure AWS PrivateLink

### Step 1: Create a Network Load Balancer (NLB)

1. Go to **AWS Management Console** → **EC2** → **Load Balancers** → **Create Load Balancer**.
2. Select **Network Load Balancer**.
3. Configure:
   - Name: `my-service-nlb`
   - Scheme: **Internal**
   - Listeners: TCP 443 (for HTTPS) or TCP 80 (HTTP)
4. Select **subnets** in the provider VPC.
5. Register targets (EC2 instances hosting your service).
6. Click **Create Load Balancer**.

---

### Step 2: Create VPC Endpoint Service

1. Go to **VPC Console** → **Endpoint Services** → **Create Endpoint Service**.
2. Select **Network Load Balancer** created earlier.
3. Enable **Acceptance Required** if you want manual approval for consumers.
4. Click **Create Endpoint Service**.
5. Note the **Service Name** (e.g., `com.amazonaws.vpce.myservice`).

---

### Step 3: Create VPC Endpoint in Consumer VPC

1. Go to **VPC Console** → **Endpoints** → **Create Endpoint**.
2. Select **Service Category**: Find the service by name (from provider’s VPC).
3. Select **VPC and Subnets** where ENI should be created.
4. Configure **Security Groups** to allow traffic to the service.
5. Click **Create Endpoint**.

---

### Step 4: Accept Endpoint Connection (If Required)

- If the provider enabled manual acceptance:
  1. Go to **Endpoint Service** → **Pending Connections**.
  2. Accept connection requests from consumers.

---

### Step 5: Test Connectivity

1. From consumer VPC, connect to the service using the **private DNS name** or ENI IP.
2. Example:
   ```bash
   curl https://myservice.vpce.amazonaws.com/api

3. Verify traffic does not traverse the public internet:

   * Check **VPC Flow Logs**.
   * Ping or curl using private IP assigned to VPC endpoint.

---

## Practical Example: Private API Access

### Scenario

You host a **REST API** on EC2 instances behind an **NLB** in **VPC-A**. Your application in **VPC-B** needs secure access to this API without exposing it publicly.

### Step 1: Provider Setup (VPC-A)

* Create **EC2 instances** with the API service.
* Create **Internal NLB** pointing to EC2 instances.
* Create **VPC Endpoint Service** for NLB (`com.amazonaws.vpce.api-service`).

### Step 2: Consumer Setup (VPC-B)

* Create **VPC Endpoint** for the service in subnets of VPC-B.
* Security group allows traffic from consumer instances to the endpoint.
* If provider requires approval, accept endpoint connection.

### Step 3: Access the API Privately

* From EC2 in VPC-B:

  ```bash
  curl https://api-service.vpce.amazonaws.com/v1/status
  ```
* The request goes through **VPC endpoint ENI** → NLB → API service in VPC-A.
* Traffic never leaves AWS private network.

---

## Best Practices

1. Use **internal NLB** to avoid public exposure.
2. Enable **DNS integration** for easier access to services.
3. Use **Security Groups** to restrict access.
4. Monitor with **VPC Flow Logs** for private endpoint traffic.
5. Enable **acceptance required** for better control over who can access your service.
6. Consider **cross-account access** carefully for multi-account architectures.

---

## Summary

AWS PrivateLink allows **secure, private, and scalable connectivity** between services across VPCs or accounts. It avoids public internet exposure, simplifies network topology, and integrates with AWS services.

**Practical Example**: Private API hosted on EC2 in one VPC can be securely accessed by consumer applications in another VPC using PrivateLink, NLB, and VPC endpoints, ensuring traffic stays within AWS private network.

---

**References**:

* [AWS PrivateLink Documentation](https://docs.aws.amazon.com/privatelink/)
* [AWS VPC Endpoint Services Overview](https://aws.amazon.com/privatelink/)
