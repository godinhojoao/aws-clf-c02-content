# AWS Overview

## AWS Cloud Pricing: 3 pricing fundamentals (following the pay-as-you-go model)

- 1. **Compute:** Pay for compute time.
- 2. **Storage:** Pay for data stored in the Cloud.
- 3. **Networking:** Data transfer IN is free and Data transfer OUT is payed.

## AWS Cloud Use cases

- Enterprise IT, Backup & Storage, Big Data Analytics
- Host website, Mobile & Social Apps
- Host gaming service

## AWS Global Infrastructure: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

- **AWS Regions:**
  - Geographical areas (North America, Sao paulo...)
  - A cluster of data centers.
  - Most AWS services are region-scoped.
  - Name can be us-east-1, etc...
  - How to choose one Region?
    - **Compliance** with data governance and legal requirements.
    - **Proximity to customers:** reduced latency.
    - **Available services:** some services are not available in every Region.
    - **Pricing:** It changes for each Region and is transparent in the service pricing page.
- **AWS Availability Zones: (AZ)**
  - Each region has many availability zones min = 3 and max = 6.
    - AWS Region Sydney ap-southeast-2
    - Availability zones: ap-southeast-2a | ap-southeast-2b | ap-southeast-2c
  - **Each AZ is:** one or more discrete data centers with redundant power, networking, and connectivity.
  - Separate, isolated locations within a Region. Turning it fault-tolerant and highly available by spreading the risk of failure.
  - They are connected with high bandwidth, ultra-low latency networking.
- **AWS Edge Locations / Points of Presence:** Sites closer to end users for faster content delivery and lower latency.

## AWS Global Services examples:

- Identity and Access Management (IAM)
- Route 53 (DNS Service)
- CloudFront (Content Delivery Network, CDN)
- WAF (Web Application Firewall)

## AWS Region-Scoped Services examples: (most AWS services)

- Amazon EC2 (Infrastructure as a Service)
- Elastic Beanstalk (Platofrm as a Service)
- Lambda (Function as a Service)
- Rekognition (Software as a Service)
- Regional Services list: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

