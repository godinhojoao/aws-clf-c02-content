# AWS Databases

## Introduction

- Storing data on disk (EBS, EFS, EC2 Instance Store, S3) can have its limits.
- You can need a structured data, with efficient queries/searches, etc.

## Shared Responsibility Model for databases

- AWS security OF the cloud:
  - Operating system patching.
  - Monitoring and alerting.
  - Provide tools to backup and restore
  - And obviously all the infrastructure.
- User security IN the cloud:
  - Securing access to the database. (User roles and privileges) -> least privilege principle
  - Configuring firewall and security groups.
  - Application-specific security -> sql injection.

## Amazon RDS - Relational Database Service

- Allow you to create relational databases managed by AWS in the cloud.
  - Examples: Postgres, MySQL, MariaDB, Oracle, Aurora (AWS Proprietary Database)
- **Advantages of using RDS instead of DB on EC2**:

  - RDS is a managed service, AWS will do the updates for you when needed.
  - Continuous backups and restore to specific timestamp (Point in Time Restore)
  - Monitoring dashboards
  - **Read replicas** for improved read performance and **high scalability**
  - **Multi AZ** for disaster recovery and **high availability**
  - Scaling capability (horizontally and vertically)
  - Storage backed by EBS - Elastic Block Store.
  - **BUT** you can't SSH into your instances.

  - ### Amazon Aurora

    - Proprietary database from AWS (not open source).
    - PostgreSQL and MySQL are both compatible with Aurora.
    - Cloud optimized, so it's much more performatic over MySQL and PostgreSQL directly on RDS.
    - Costs more than RDS (20% more), but is more efficient.
    - Not in the free tier.
    - **Amazon Aurora Serverless**:
      - Automated database instantiation and auto-scaling based on actual stage.
      - Least management overhead.
      - Pay per second, can be more cost effective for **use cases**:
        - Infrequent access;
        - Intermittent or unpredictable workloads;

  - ### AWS RDS Deployment Options
  - **Read replicas**:
  - Scale the workload of your DB. (can create 15 read replicas)
  - Application write just to the main database and it is replicated to the read replicas.
  - **Multi AZ**: Failover DB
    - Failover in case of AZ crashing. (high availability)
    - Replication **Cross AZ** -> **Failover DB**.
    - Can have only 1 other AZ as failover.
  - **Multi Region**: (Read replicas)
    - Write by the application is still cross region, but the read will be made in the same region reducing latency.
    - The main db is the only one written.
    - Good Disaster Recovery since you have more than one region with same data replicated.

## AWS ElastiCache

- Redis or Memcached managed by AWS.
- Caches are in-memory databases with high performance and low latency.
- Helps to reduce load off databases for read intensive workloads.

## AWS DynamoDB

- Key/value NoSQL database. You have `tables -> items with (key/value)`
- Fully managed highly available with replication across 3 AZ.
- Scales to massive workloads, distributed "serverless" database.
  -> There are still servers in the back but we don't need to select the instance type as we do with Amazon RDS.
- Millions of requests per seconds, trillions of row, 100s of TB of storage.
- Performatic, low latency (single-digit millisecond latency retrieval)
- Low cost and auto scaling capabilities.
- Standard & Infrequent Access (IA) Table Class.

  - ### DAX - DynamoDB Accelerator

    - Fully managed in-memory cache that's specific for DynamoDB.
    - Very well integrated with DynamoDB.
    - 10x performance improvement.

  - ### DynamoDB Global Tables
    - Make a DynamoDB table accessible with **low latency** in **multiple-regions**.
    - Replicate DynamoDB in another region to reduce latency.

## Amazon Redshift -> Database to do analytics and data visualization

- Based on Postgres but focused on OLAP - Online analytical processing.
- Has a SQL interface to do queries.
- Good for integrating with BI tools such as Tableau or PowerBI.

  - ### Redshift serverless
    - Don't need to manage manually clusters, node type, size, and all infrastructure configuration.
    - Pay for only what you use.

## Amazon EMR - Amazon Elastic MapReduce
- To create **Hadoop clusters (Big Data)** to analyze and process vast amount of data.
- The clusters can be made of hundreds of EC2 instances.
- EMR takes care of all the provisioning and configuration.
- Auto-scaling and integrated with Spot instances.
- **Use cases**: Data processing, machine learning, big data...

## Amazon Athena -> Serverless query service to perform analytics
- Serverless **query service to perform analytics against S3 objects.**
- Uses SQL language to query the files.
- Supports CSV, JSON, ORC, and more.
- **Use cases**: Business intelligence, analytics, reporting, analyze & query VPC logs, ELB Logs, CloudTrail trails, etc..
- **Exam tip**: Analyze data in S3 using serverless SQL, use athena.

## Amazon QuickSight
- Serverless machine learning-powered business intelligence service to create interactive dashboards.
- **Use cases**: Business analytics, building visualizations, get business insights using data.
- Integrated with RDS Aurora, Athena, Redshift, S3...

## Amazon DocumentDB
- Aurora is an "AWS-implementation" of PostgreSQL/MySQl...
- DocumentDB is the same for MongoDB.
- Similar "deployment concepts" as Aurora. Fully managed database, highly available with replication across 3 AZ.

## Amazon Neptune -> Graph Database
- Fully managed **Graph Database**.
- A popular dataset would be a **social network**
  - Users have friends
  - post have comments
  - comments have likes from users
  - Users share and like posts...
- Optimized for complex and hard queries with highly connected datasets.
- Can store up to billion of relations and query the graph with milliseconds latency.
- Highly available across 3 AZ, with up to 15 read replicas.
- **Use cases**: social networks, knowledge graphs (wikipedia), recommendation engines, and more...

## Amazon Timestream
- Fully managed, serverless time series database.
- Store and analyze trillions of events per day.
- Built-in time series analytics functions to help you identify patterns in your data in near real-time.

## Amazon QLDB - Ledger (financial)
- Fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log owned by a central trusted authority.
- Amazon QLDB tracks each and every application data change and maintains a complete and verifiable history of changes over time.

## Amazon Managed Blockchain
- It makes possible to build applications where multiple parties can execute transactions without the need for trusted central authority. So there's a decentralization aspect to a Blockchain.
- Amazon Managed Blockchain is a managed service to:
  - Join public blockchain networks
  - Or create your own scalable private network

## Amazon Glue
- Managed extract, transform, and load (ETL) service.
- Useful to prepare and transform data for analytics.
- Fully serverless service.
- Example of use case:
  - Extract data from S3 and Amazon RDS -> transform the data -> load data into a Redshift Database to analyze.
- **Glue Data Catalog**:
  - Central repository to store structural and operational metadata for all your data assets.

## Amazon DMS - Database Migration Service
- Quickly and secure migrate databases to AWS, resilient, self healing.
- The source database remains available during the migration.
- Support:
  - Homogeneous migrations: Oracle to Oracle.
  - Heterogeneous migrations: Microsoft SQL Server to Aurora.

## !Important
- Dynamodb is a great option to store data for a recommendation engine with LEAST operational overhead.
- RDS and other databases:
  - **Read replica single-AZ**: High Scalability
  - **Multi-AZ / multi-region**: High Availability (fault tolerance)

## Reference

- https://aws.amazon.com/rds/
- https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html
- https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html
- https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.html
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html
- https://docs.aws.amazon.com/redshift/latest/mgmt/welcome.html
- https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html
- https://docs.aws.amazon.com/athena/latest/ug/what-is.html
- https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html
- https://docs.aws.amazon.com/neptune/latest/userguide/intro.html