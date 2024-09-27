## AWS S3 - Simple Storage Service

- One of the main building blcok of AWS.
- Advertised as "Infinitely scaling" storage.
- Many websites uses AWS S3 as backbone (foundational resource).
- Many AWS Services use Amazon S3 as an integration as well.

- ## Use cases
- Backup and storage, disaster Recovery, archive..
- Hybrid Cloud Storage (on-premise + cloud s3 as storage)
- **Hosting**: Static websites, applications, media, etc...

- ## Amazon S3 - Buckets
- Allows people to store objects (files) in "buckets" (directories).
- Buckets must have a globally unique name (across all regions and all accounts).
- Buckets are defined at the region level, S3 looks like a global services but buckets are in a region.
- Naming convention:

  - No uppercase, no underscore
  - 3-63 characters long
  - Not an IP
  - Must start with lowercase letter or number
  - Must NOT start with the prefix xn--
  - Must NOT end with the suffix -s3alias

- ## Amazon S3 - Objects
- Objects (files) have a key:
  - The key is FULL path: **prefix + object name**
  - Example: `s3://my-bucket/my_file.txt`
- Objects are the content of the body:

  - Max. Object size 5TB
  - If uploading more than 5GB, must use "multi-part upload"
  - Metadata (list of text key / value pairs - system or user metadata)
  - Tags (Unicode key / value pair - up to 10) - useful for security / lifecycle
  - Version ID (if versioning is enabled)

- ## Amazon S3 - Security
- **User-Based**: IAM Policies - which API calls should be allowed for a specific user from IAM.
- **Resource-Based**:
  - Bucket Policies - bucket wide rules from S3 console - allows across account
  - Object Access Control List (ACL) - finer grain (can be disabled)
    - When you have specific rules for an object, example: just one user can access this object.
  - Bucket Access Control List (ACL) - less common (can be disabled)
- **Encryption**: Encrypt objects in Amazon S3 using encryption keys.s
- **How to allow or deny access**:

  - Same account users: You can basically allow by IAM attaching IAM policies to the user.
  - Public access (any site): S3 Bucket policy to allow public access.
  - Instance access (EC2): IAM Roles for the instance.
  - Cross-Account Access: Use s3 Bucket policy to allow cross-account access.

- ## Amazon S3 - Static Website Hoisting
- S3 can host static sites and have them accessible on the Internet.
- The website URL will be (depending on the region)
  - http://bucket-name.s3-website-aws-region.amazonaws.com OR
  - http://bucket-name.s3-website.aws-region.amazonaws.com
- If you get 403 Forbidden error, make sure the bucket policy allows public reads.
- **Steps:**

  - On your S3 Bucket -> properties -> ENABLE Static website hosting
  - Then upload a index.html file and allow public access on your bucket policies.

- ## Amazon S3 - Versioning
- You can version your files in Amazon S3. It is enabled at the **bucket level**.
- Same key overwrite will change the "version" 1, 2,3...
- It is best practice to version your buckets.

  - Protect to unintended deletes (ability to restore a version)
  - Easy roll back to previous version.
  - You need to enable versioning and if you disable it will not delete your previous versions.

- ## Amazon S3 - Replication
- Must enable Versioning in source and destination buckets. And must give proper IAM permissions to S3.
- Buckets can be in different AWS accounts.
- Copying is asynchronous.
- **CRR - Cross Region Replication**: compliance, lower latency access, replication across accounts.
- **SRR - Same Region Replication**: log aggregation, live replication between production and test accounts.

- ### How to create a replication rule inside your S3 bucket:

  - `your bucket -> management -> replication rules -> create replication rule`
  - Now if you upload something in your bucket it will be replicated to the destination bucket.

- ## Amazon S3 - Storage Classes
- We can **move objects between classes** manually or using s3 lifecycle configurations.
- You can configure a lifecycle configuration on: `your bucket -> management -> lifecycle rules -> create lifecycle rule`
- **Durability on s3**: If you store 10 million objects on Amazon S3, you can expect losing 1 after 10 thousand years.
- **Availability on s3**: Measure how readily available a service is. EX: S3 standard 99.99% availability = 53 minutes off a year

- ### Amazon S3 Standard:

  - General purpose; Use cases: Mobile, big data analytics, content distribution, gaming...
  - High availability (99.99%);
  - frequently accessed data;
  - low latency and high throughput;
  - sustain 2 concurrent facility failures

- ### Amazon S3 Standard-Infrequent Access (IA):

  - Usecases: Disaster recovery, backups.
  - Same as standard but for data that is less frequently accessed, but requires rapid access when needed.
  - Lower cost than S3 Standard.

- ### Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA):

  - Usecases: Storing secondary backup copies of on-premise data, or data you can recreate.
  - High durability (99.99%) in a single AZ; Data lost when AZ is destroyed. (not good for disaster recovery)
  - 99.5% availability.

- ### Amazon S3 Glacier Storage Classes:

  - Low-cost object storage meant for archiving/backup.
  - Pricing: storage + object retrieval cost.
  - **S3 Glacier Instant Retrieval**:
    - Millisecond retrieval, great for data accessed once a quarter
    - Minimum storage duration of 90 days.
  - **S3 Glacier Flexible Retrieval (Amazon S3 Glacier)**:
    - Time to retrieve data: Expedited (1 to 5 minutes), Standard (3 to 5 hours), Bulk (5 to 12 hours) - free.
    - Minimum storage duration of 90 days.
  - **S3 Glacier Deep Archive**:
    - For long term storage.
    - Time to retrieve data: Standard (12 hours), Bulk (48 hours)
    - Minimum storage duration of 180 days.

- ### Amazon S3 Intelligent-Tiering

  - Small monthly monitoring and auto-tiering fee.
  - Moves objects automatically between Access Tiers based on usage.
  - There are no retrieval charges in S3 Intelligent-Tiering.
  - **Frequent Access tier (automatic)** - default tier.
  - **Infrequent Access tier (automatic)** - objects not accessed for 30 days.
  - **Archive Instant Access tier (automatic)** - objects not accessed for 90 days.
  - **Archive Access tier (optional)** - configurable from not accessed for 90 days to 700+ days.
  - **Deep Archive Access tier (optional)** - configurable from not accessed for 180 days to 700+ days.

- ## Amazon S3 Encryption:
- Server-Side encryption **(default)**.
  - Server encrypts the file after receiving it.
  - When an user upload a file on S3 it is encrypted by default for security purposes.
- Client-Side encryption:

  - User encrypts the file before uploading it.

- ## IAM Access Analyzer for S3
- Ensures that only intendend people have access to your S3 buckets.
- It alerts you to confirm if it's normal or a security issue, and you can reconfigure access if needed.

## Shared Responsibility Model for S3

- AWS -> security OF the cloud:
  - Infrastructure (global network, durability, availability, sustain concurrect loss of data in two facilites).
  - Configuraiton and vulnerability analysis.
  - Compliance validation.
- USER -> security IN the cloud:
  - S3 versioning.
  - S3 bucket policies.
  - S3 Replication Setup.
  - Logging and Monitoring.
  - S3 Storage Classes
  - Data encryption at rest and in transit.

## AWS Snow Family

- Physical devices and services from AWS designed to help with data transfer and edge communication in various scenarios.
- Highly-secure, portable devices to collect and process data at the edge, and **migrate data** into or out AWS.
- **AWS Snowcone**: Smaller device with less storage, but still a lot of storage: 8TB - 14TB SSD. -> migrate terabytes TB
- **AWS Snowball**: Bigger device with more storage, 80TB - 210TB. -> migrate petabytes PB
- **AWS Snowmbile**: Biggest device with more storage, 100PB. -> migrate exabytes EB
- **Usecase**: If you need to migrate data.
  - If you are migrating a lot of data, it will take a lot of time.
  - You can loss connectivity, and more..
  - Snow family are offline devices to perform data migrations.
  - For more than a week to transfer over the network -> Snow Family devices.
- **How it works**: You transfer it locally to a Snow Family device, then this device transfer to an Amazon S3 Bucket.
- **Usage Process**

  - 1. Request Snowball devices from the AWS console for delivery.
  - 2. Install the snowball client/AWS OpsHub on your servers. -> desktop application to manage Snow Family devices.
  - 3. Connect the snowball to your servers and copy files using the client.
  - 4. Ship back the device when you're done (goes to the right AWS facility).
  - 5. Data will be loaded into an S3 Bucket.
  - 6. Snowball is completely wiped.

- ## What is Edge Computing?
- Process data while it's being created on a **edge location**.
  - A truck on the road, a ship on the sea, a mining station underground... (with bad connectivity)
- These locations may have limited internet and no access to computing power.
- We setup a **Snow Family Device** to do **Edge Computing**.
- **Usecases**: Preprocess data, machine learning, transcoding media.

- ## AWS Snowball Edge - Pricing
- You pay for **device usage** and **data transfer out AWS**.
- **Data transfer IN** to Amazon S3 is free.
- **On-demand**:
  - One time service fee based on your usage. 10days 80TB or 15 days 210TB.
- **Commited Upfront**:
  - Pay in advance for monthly, 1-year, and 3-years of usage **(Edge computing)**.
  - Up to 62% discounted pricing.

- ## Hybrid Cloud for Storage
- AWS is pushing for "hybrid cloud".
  - Part of your infrastructure is on-premise.
  - Part of your infrastructure is on the cloud.
- This can be due to:
  - Long cloud migrations.
  - Security requirements.
  - Compliance requirements.
  - IT strategy.
- S3 is a proprietary storage technology (unlike EFS/NFS), so how do you expose the S3 data on-premise?
  - **AWS Storage Gateway**

- ### AWS Storage Cloud Native Options
  - Block: Amazon EBS or EC2 Instance Store
  - File: Amazon EFS
  - Object storage: Amazon S3 or Glacier

- ### AWS Storage Gateway
  - Bridge between on-premise data and cloud data in Amazon S3.
  - Hybrid storage to seamlessly use the AWS Cloud.
  - Use cases: disaster recovery, backup & restore, tiered storage.
  - **Types of Storage Gateway**: (not important to know for cloud practicioner)
    - File gateway; Volume gateway; Tape gateway
    - Behind the scenes it is using: EBS, S3 and Glacier

## !Important
- **Encryption by default**: AWS Storage Gateway && Amazon Simple Storage Service (Amazon S3)
- **AWS Macie**: Machine learning to discover and protect data and also **AWS S3** (security and data privacy service).
- **S3 One Zone-Infrequent Access (S3 One Zone-IA)**: less frequent access but needs to be fast when needed.

## Reference

- https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/glacier-storage-classes.html
- https://docs.aws.amazon.com/snowball/latest/developer-guide/getting-started.html