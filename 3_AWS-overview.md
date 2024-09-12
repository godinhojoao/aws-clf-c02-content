# AWS Overview

## AWS Cloud Pricing: 3 pricing fundamentals (following the pay-as-you-go model)

- 1. **Compute:** Pay for compute time.
- 2. **Storage:** Pay for data stored in the Cloud.
- 3. **Networking:** Data transfer IN is free and Data transfer OUT is payed.
  - Receiving a HTTP post with a JSON payload -> free
  - Sending a HTTP JSON response -> payed

## AWS Cloud Use cases

- Enterprise IT, Backup & Storage, Big Data Analytics
- Host website, Mobile & Social Apps
- Host gaming service

## AWS Global Infrastructure: https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

- **AWS Regions:**
  - Independent Geographical Areas (North America, Sao paulo...). With a cluster of datacenters within this geographical area.
  - Most AWS services are region-scoped. Name can be us-east-1, etc...
  - How to choose one Region?
    - **Compliance** with data governance and legal requirements.
    - **Proximity to customers:** reduced latency.
    - **Available services:** some services are not available in every Region.
    - **Pricing:** It changes for each Region and is transparent in the service pricing page.
- **AWS Availability Zones: (AZ)**
  - One or more data centers with redundant power, networking, and connectivity.
  - Separated, isolated locations within a Region. Turning it fault-tolerant and highly available by spreading the risk of failure.
  - They are connected with high bandwidth, ultra-low latency networking.
  - Each region has many availability zones min = 3 and max = 6.
    - AWS Region Sydney ap-southeast-2
    - Availability zones: ap-southeast-2a | ap-southeast-2b | ap-southeast-2c
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

## [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)

- It is a framework to delineates the responsibilites of AWS as a cloud provider service and the responsibilites of the customers using AWS services, dividing security and compliance duties between AWS and its customers.

<img src="./images/Shared_Responsibility_Model_V2.jpg" alt="AWS Shared Responsibility Model"/>

- ## AWS responsibility "Security of the Cloud":
- AWS is responsible for protecting the infrastructure that runs all of the AWS services.
- This infrastructure is composed of the hardware, software, networking, and facilities that run AWS Cloud services.

- ## Customers responsibility "Security in the Cloud":
- Customer responsibility will be determined by the AWS Cloud services that a customer selects.
- **For a service such as Amazon Elastic Compute Cloud (Amazon EC2)** that is categorized as Infrastructure as a Service (IaaS) and, as such, requires **the customer to perform all of the necessary security configuration and management tasks.**
  - Management tasks on each instance: Updating operating system, database, and any other software. And also configuring AWS-provided firewall, called "security group".
- For **abstracted services**, such as Amazon S3 and Amazon DynamoDB, AWS operates the infrastructure layer, the operating system, and platforms, and **customers access the endpoints to store and retrieve data**.
  - Customers are responsible for managing their data (including encryption options), classifying their assets, and using IAM tools to apply the appropriate permissions.

- ## This customer/AWS shared responsibility model also extends to IT controls:
- **Inherited Controls:** Which a customer fully inherits from AWS.
  - Physical and Environmental controls
- **Shared Controls:** Which apply to both the infrastructure layer and customer layers, but in completely separate contexts or perspectives. **AWS provides** the requirements for the infrastructure and the **customer must provide** their own control implementation within their use of AWS services.
  - **Patch Management** AWS is responsible for patching and fixing issues within the infrastructure, but customers are responsible for patching their guest OS and applications.
  - **Configuration Management:** AWS maintains the configuration of its infrastructure devices, but a customer is responsible for configuring their own guest operating systems, databases, and applications.
  - **Awareness & Training:** AWS trains AWS employees, but a customer must train their own employees.
- **Customer Specific:** Which are exclusively the responsibility of the customer based on how they use AWS services.
  - Service and Data Security: Customers may need to manage how data is routed and secured within specific environments.
