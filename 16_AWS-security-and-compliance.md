# AWS Security and Compliance

## DDoS Attack - AWS WAF and Shield

- **AWS Shield Standard**: Protects against DDoS Attack for your website and application, for all customers at no additional costs.
- **AWS Shield Advanced**: 24/7 Premium DDoS protection.
- **AWS WAF - Web Application Firewall**: Filter sepcific requests based on rules.
- **AWS CloudFront and Route53**:
  - Availability protection using global edge network.
  - Combined with AWS Shield, provides attack mitigation at the edge.
- Being ready to scale: **AWS Auto Scaling** and **ELB - Elastic Load Balancing**.

## AWS Shield - (Layer 4 - TCP/UDP) -> ONLY used to protect running applications from DDoS attacks.

- Free service for every AWS customer.
- Provides protection against layer 3 and 4 DDoS attacks, including SYN and UDP floods.

## AWS WAF - Web Application Firewall (Layer 7 - HTTP)

- Protects your web application from common web exploits (Layer 7).
- Layer 7 - HTTP. So can be deployed on Application Load Balancer, API Gateway, CloudFront.
- **Define WebACL (Web Access Control List)**
  - Rules can include IP Addresses, HTTP Headers, HTTP Body, or URI strings.
  - Protects from common attack such as SQL Injection and Cross-Site Scripting (XSS)
  - Size constraints (to avoid big requests), geo-match (block countries)
  - Rate-based rules (to count occurrences of events) - for DDoS protection -> rate limit.

## AWS Network Firewall - (Protect your entire Amazon VPC)

- From layer 3 to Layer 7 protection
- Any direction, you can inspect:
  - VPC to VPC
  - Outbound to internet
  - Inbound to internet
  - To/from Direct Connect and Site-to-Site VPN

## AWS Firewall Manager - if you need to meet compliance and security needs within an AWS organization / AWS account

- Manage security rules in all accounts of an AWS Organization. (WAF, SHIELD...)
- Security policy: common set of security rules
  - **VPC Security Groups for EC2**, Application Load Balancer, etc...
  - WAF rules
  - AWS Shield Advanced
  - AWS Network Firewall
- Rules are applied to new resources as they are created. Good for compliance.

## Penetration testing on AWS Cloud

- There are some services in which you can test without asking approval:
  - Amazon EC2 instances, NAT Gateways, Load balancers, Amazon RDS, CloudFront, etc..
- But some kinds of attacks you are prohibited to do: (normally DDoS attacks in general)
  - You **can't do DDoS Attacks on your own infrastructure within AWS** because it seems that you want to attack AWS itself.

## Encryption of data

- We want to encrypt both **data at rest** and **data in transit**.
- For it we use **encryption keys**. In which even if someone have your encrypted data it can't be read.

### Encryption - Data at rest

- Stored or archived on a physical device.
  - Hard disk, RDS instance, S3 Glacier Deep Archive, etc..

### Encryption - Data in transit

- Data being moved from one location to another. Transferred over the network.
  - Transfer from on-premise to EC2 to DynamoDB, etc..

### AWS KMS - Key Management Service

- AWS manages the encryption keys for us.
- Create and control keys used for cryptographic operations
- Encryption Opt-in:
  - EBS volumes: encrypt volumes.
  - S3 buckets: Server side encryption of objects.
  - Redshift database: encryption of data.
  - RDS database: encryption of data.
- Encryption automatically enabled:
  - CloudTrail Logs.
  - S3 Glacier.
  - Storage Gateway.
- **Types of keys**:
  - **Customer Managed Key**:
    - Created, managed and used by the customer, can enable or disable.
    - Rotation policy (new key generated every year).
    - Possibility to bring your own key.
  - **AWS Managed Key**:
    - Created, manged and used on the customer's behalf by AWS.
    - Used by AWS services (key names: aws/s3, aws/ebs, aws/redshift)
  - **AWS Owned Key**:
    - Collection of keys that an AWS service owns and manages to use in multiple accounts.
    - AWS can use them to protect resources in your account. (but you can't view the keys)

### AWS CloudHSM - Hardware Security Module

- AWS provisions encryption hardware that we manage ourselves, not by AWS.
- **Encryption Keys (custom keystore)**:
  - Keys generated from your own CloudHSM hardware device.
  - Cryptographic operations are performed within the CloudHSM cluster.

## AWS Certificate Manager (ACM)

- Let's you easily provision, manage, and deploy SSL/TLS certificates.
- Used to provide in-flight encryption for websites (HTTPS).
- Free of charge for public TLS certificates.
- Automatic TLS certificate renewal.
- Integrations with
  - Elastic Load Balancer
  - CloudFront Distributions
  - APIs on API Gateway
- **How it works**
  - EC2 instances -> Application Load Balancer <-> AWS Certificate Manager (provision and maintains TLS certs) -> user access https

## AWS Secrets Manager

- For storing secrets.
- Capability to force rotation of secrets every x days.
- Automate generation of secrets on rotation (with Lambda).
- Integration with Amazon RDS (MySQL, PSQL, Aurora)
- Secrets are encrypted using KMS
- Mostly meant for RDS Integration

## AWS Artifact (not really a service)

- Portal thal provides customers with on-demand access to **AWS security and compliance documentation** and AWS agreements
- Can be used to support internal audit or compliance.
- **Artifact Reports**:
  - Download AWS security and compliance documents from third-party auditors, like AWS ISO certifications, Payment Card Industry (PCI), and System Organization Control (SOC) reports.
- **Artifact Agreements**:
  - Allows you to review, accept, and track the status of AWS Agreements such as the Business Associate Addendum (BAA) or the Health Insurance Portability and Accountability Act (HIPAA) for an individual account or in your organization.

## Amazon GuardDuty -> (Threat detection that is always monitoring activity and unauthorized behavior)

- Intelligent Threat discovery to protect your AWS Account.
- Uses Machine Learning algorithms, anomaly detection, 3rd party data.
- One click to enable (30 days trial), no need to install software.
- Can also setup **EventBridge rules** to notify in case of finding something.
  - EventBridge rules can target AWS Lambda or SNS.
- Input data includes:
  - CloudTrail Events Logs: unusual API calls, unauthorized deployments
    - CloudTrail Management Events - Create VPC subnet, create trail...
    - CloudTrail S3 Data Events - get object, list objects, delete object...
  - VPC Flow Logs: unusual internal traffic, unusual IP addresses
  - DNS Logs: compromised EC2 Instances sending encoded data within DNS queries
  - Optional Features: EKS Audit Logs, RDS and Aurora, EBS, Lambda, S3 Data Events...

## Amazon Inspector (Automated Security Assessments)

- **Continuous scanning of the infrastructure trying to find vulnerabilities**.
- A risk score is associated with all vulnerabilities for priorization.
- Reporting and integration with **AWS Security Hub**. **Also send findings to Amazon EventBridge**.
- Usage Examples: (only for EC2, Container Images and Lambda Functions)
  - For EC2 Instances:
    - Uses the AWS Systems Manager (SSM) agent to analyze against OS known vulnerabilities, network, etc..
  - For Container Images push to Amazon ECR: Assessment of Container Images as they are pushed.
  - For Lambda Functions: Analyze software vulnerabilities, dependencies (packages), etc..

## AWS Config - (Records the configuration and changes over time.)

- Helps with auditing and recording compliance of AWS resources.
- Possibility to store configuration data in S3 (analyzed by Athena).
- Questions that can be solved by AWS Config:
  - Is there unrestricted SSH access to my security groups?
  - Do my buckets have any public access?
  - How has my ALB configuration changed over time?
- You can receive alerts (SNS notifications) for any changes.
- AWS Config is a per-region service.
- Can be aggregated across regions and accounts.

## AWS Macie - Discover Sensitive Data (PII - Personally Identifiable Information)

- Macie helps identify and alert you to sensitive data, such as Personally Identifiable Information (PII)
- Data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.
- **How it works**:
  - **S3 buckets** data is analyzed by **AWS Macie** and if is there any sensitive data notify your **EventBridge**.

## AWS Security Hub

- **Central security tool** to manage security across several AWS accounts and **automate security checks**.
- Integrated dashboards showing current security and compliance status to quickly take actions.
- To work you first need to enable AWS Config Service.
- Automatically aggregate alerts in predefined or personal findings formats from various AWS Services and AWS Partner tools:
  - Config
  - GuardDuty
  - Inspector
  - Macie
  - IAM Access Analyzer
  - AWS Systems Manager
  - AWS Health
  - AWS Partner Network Solutions
- Example: <img src="https://d1.awsstatic.com/Digital%20Marketing/House/Hero/products/Security%20Hub/Product-Page-Diagram_AWS-Security-Hub%402x.7e7c0483e9ce1507af2e9214247a1825a27d6bde.png">

## Amazon Detective - (identifies the root cause of security issues)
- GuardDuty, Macie, and Security Hub are used to identify potential security issues.
- Sometimes security findings require deeper analysis to isolate the root cause and take action - complex process.
- Amazon Detective analyzes, investigates, and quickly **identifies the root cause of security issues** or suspicious activites (using Machine Learning and graphs).
- Automact collects and processes events from VPC Flow Logs, CloudTrail, GuardDuty and create a unified view.
- Produces visualizations with details and context to get the root cause.

## AWS Abuse
- Report suspected AWS resources used for abusive or illegal purposes
- **Abusive and Prohibited behaviors are**:
  - **SPAM** - receiving undesired emails from AWS-Owned Ip address websites.
  - **Port scanning** - sending packets to your ports to discover the unsecured ones.
  - **DDoS Attack** - AWS-Owned IP Address attempting to overwhlem or crash your servers.
  - **Intrusion / attempts** - loggin in on your resources.
  - **Distributing malware** - AWS resources distributing software to harm computers or machines.
  - **Host Illegal or Copyrighted content**
- Contact the AWS Abuse team.

## Root User Privileges (Account Owner, created together with the AWS account)
- Complete access to all AWS services and resources.
- Do not use Root account for everyday tasks, even administrative tasks.
- **Actions that only root user can do**:
  - Change account settings (name, address, root user password and access keys).
  - View certain tax invoices.
  - Close your AWS Account.
  - Restore IAM user permissions.
  - Change or cancel your AWS Support Plan.
  - Register as a seller in the Reserved Instance Marketplace.
  - Configure an Amazon S3 Bucket policy that includes an Invalid VPC ID or VPC endpoint ID.

## IAM Access Analyzer
- **Find out which resources are shared externally**
  - S3 buckets
  - IAM Roles
  - KMS Keys
  - Lambda Functions and Layers
  - SQS Queues
  - AWS Secrets Manager
- **Zone of Trust**: AWS Account or AWS Organization
  - Reports and blocks access attempts from outside the Zone of Trust.
  - For example, if an external client tries to access an S3 bucket within the Zone of Trust, it will be blocked and flagged as a security risk.

## !Important
- **MFA with physical device**: U2F security key
- **MFA without physical device**: Virtual Multi-Factor Authentication (MFA)
- **CloudTrail**: See if the company meets the **governance, compliance and auditing norms**.
- **AWS Artifact**: Provides AWS **security and compliance documentation** with **REPORTS** and etc.
- **AWS Shield**: is a global service.
- **AWS WAF**: web common vulnerabilities and can also block geographies.