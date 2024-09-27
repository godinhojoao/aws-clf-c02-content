# AWS Using the global infrastructure

## Global Applications

- A global application is an application deployed in multiple geographies. On AWS this could be Regions or Edge Locations.
- Decreased lattency and disaster recovery.
- **Global DNS -> Route 53**:
  - Great to route users to the closest deployment with least latency.
  - Great for disaster recovery strategies.
- **Global Content Delivery Network (CDN)-> CloudFront**:
  - Replicate part of your application to AWS Edge Locations - decrease latency.
  - Cache common requests - improved user experience and decreased latency.
- **S3 Transfer Acceleration**:
  - Accelerate global uploads and downloads into Amazon S3
- **AWS Global Accelerator**:
  - Improve global application availability and performance using the AWS global network.

## AWS Amazon Route 53

- A managed DNS service.
- Examples of DNS common records:
  - www.google.com -> 12.34.56.78 == **A record = hostname to IPV4**
  - www.google.com -> 2001:0db8:85a3:0000:0000:8a2e:0370:7334 == **AAAA record hostname to = IPV6**
  - search.google.com -> www.google.com == **CNAME = hostname to hostname**
  - example.com -> AWS resource == Alias (ex: ELB, CloudFront, S3, RDS...)
- **How Route 53 DNS works (summary)**:
  - 1st the client requests for an A record `myapp.mydomain.com`.
  - 2nd the route 53 send back the IP.
  - 3rd the client use this IP to reach out the correct server.
- **Route 53 Routing Policies (summary)**:

  - **Simple routing policy**:
    - Client asks for a domain `myapp.com` and route 53 returns the ip. No health checks.
  - **Weighted routing policy**:
    - Route 53 distribute the traffic between multiple EC2 instances (a kind of load balancing). With health checks.
  - **Latency routing policy**:
    - Route 53 will return the ip of the closest server to the user.
  - **Failover routing policy**: (disaster recovery)

    - We have two EC2 instances: the `primary` and the `failover`.
    - Route 53 will do a health check on the primary and if the primary fails it reachs the failover instance.

  - ### Important: ELB vs Route 53 Weighted Routing Policy
    - **Use ELB if**:
      - You want to **balance traffic** between instances or services **within a single region**.
      - You need to inspect requests and use layer 7 features like path-based routing or SSL termination.
    - **Use Route 53 (Weighted Routing) if**:
      - You want to **split traffic** between **multiple global resources or across regions**.
      - You want to route traffic at the **DNS level**, which happens before the request reaches any application-level service.

## Amazon CloudFront (CDN) -> GLOBAL DISTRIBUTION

- A content delivery network. That improve read performance, caching content in the edge.
- DDoS protection, integration with Shield, AWS Web Application Firewall.
- **Usage example**:

  - We have an S3 Bucket on Australia and one user asks for an Object of this Bucket in Canada.
  - CloudFront has 216 points of presence globally (Edge Locations) in which this Bucket can be cached.

  - ### CloudFront vs S3 Cross Region Replication
    - **CloudFront**:
      - Global Edge network.
      - Files are cached for a TTL (maybe a day).
      - Great for static content that must be available everywhere.
      - After the first fetch the data is cached and it makes the fetch much faster.
    - **S3 Cross Region Replication**:
      - Must be setup for each region you want replication.
      - Files are updated in near real-time. Read only.
      - Great for dynamic content that needs to be available at low-latency in few regions.

## AWS Transfer Acceleration

- Use to speed up the transfer of files on S3 when you want to transfer files all around the world (globally).
- It is made sending the file to an Edge Location (geographically closer to the user) and then this Edge Location will forward the data to the S3 Bucket in the target region.
- **Example**: A user on USA trying to upload an S3 file in a bucket located in Australia.
  - File goes to the USA Edge Location -> USA Edge Location forwards to the Region S3 Bucket using the AWS global network (much faster than the user network).

## AWS Global Accelerator

- Improve global applicaton **availability** and **performance** using the AWS global network.
- Leverage the AWS internal network to optimize the route to your application (60% improvement).
- **2 anycast IP** are created for your application and traffic is sent trough Edge Locations.
- **How it works**: You want to access an API far from you.
  - You will access an Edge Location
  - The Edge Location will route the traffic to the right server.

  ### - AWS CloudFront vs AWS Global Accelerator:
    - Both use the AWS Global network and its edge locations arount the world.
    - Both services integrate with AWS Shield for DDoS protection.
    - But **CloudFront**:
      - is a **Content Delivery Network (CDN)**
      - improve performance for your cacheable content (such as images and videos - static content)
      - Content is **served at the edge**
    - And **AWS Global Accelerator**
      - No caching, **proxying packets** at the edge to applications running in one or more AWS Regions.
      - Improves performance for a wide range of applications over TCP or UDP.
      - Good for HTTP use cases that require static IP addresses.
      - Good for HTTP use cases that requires deterministic, fast regional regional failover.

## AWS Outposts
- The way you have to have **your own on-premise servers from AWS**.
- **Outpost Racks** are "server racks" that offers the same AWS infrastructure, services, APIs and tools to build your own applications on-premises just as in the cloud.
- AWS will setup and manage Outposts Racks within your on-premises infrastructure.
- You are responsible for the Outposts Racks physical security.
- **Benefits**
  - Low-latency access to on-premises systems.
  - Local data processing.
  - Easier migration from on-premises to cloud.
  - Fully managed service.
  - Some services that work on Outposts:
    - EC2, EBS, S3, EKS, ECS, RDS, EMR

## AWS WaveLength Zones - Ultra-low latency (Network) zones
- WaveLength Zones are infrastructure deployments embedded within the telecommunications providers datacenters at the edge of the 5G networks.
- Brings AWS services to the edge of the 5G networks
- Ultra-low latency applications through 5G networks.
- Use cases: mobile, vehicles, real-time gaming, etc.. Everything that requires ultra-low latency.

## AWS Local Zones
- Places AWS compute, storage, database, and other selected AWS services closer to end users to run latency-sensitive applications.
- Extend your VPC to more locations - "extension of an AWS Region".
- Compatible with EC2, RDS, ECS, EBS, ElastiCache...
- **Example**:
  - AWS Region: N. Virginia (us-east-1)
  - AWS Local Zones: Boston, Chicago, Dallas, Houston, Miami, ... (you can extend this Region for these local zones)

## Global Application Architecture
- **Single Region**:
  - [ ] High availability
  - [ ] Improved Global Latency
  - [X] Easy to configure and deploy
- **Single Region, Multi AZ**:
  - [X] High availability
  - [ ] Improved Global Latency -> no, because is same region
  - [X] Medium to configure and deploy (medium)
- **Multi Region, Active-Passive**:
  - **Active**: Region in which users can write/read from.
  - **Passive**: Region in which users can only read from.
  - [X] Improved Global **Read Latency**
  - [ ] Improved Global **Write Latency** -> Not global, because one Region is only read.
  - [X] Higher difficulty to setup

## !Important
- **AWS Local Zones**: Low latency to end users. **compute and storage closer to users**
- **AWS Wavelength**: Ultra-low latency 5g **mobile, etc..**

## Reference

- https://www.cloudflare.com/learning/cdn/glossary/anycast-network/
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html
- https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration.html
- https://www.youtube.com/watch?v=Docl4julOQw&ab_channel=AmazonWebServices
- https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html
- https://aws.amazon.com/wavelength/faqs/
- https://aws.amazon.com/about-aws/global-infrastructure/localzones/features/
https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html