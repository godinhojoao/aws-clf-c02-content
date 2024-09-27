# Basics

## How do websites works?

- Client make a Network request to a Server.
- Servers are made of:
  - Compute: CPU + Memory RAM = "Brain"
  - Database: Store data in a structured way ("long-term", hard-disk)
- Network: Cables, routers and servers connected with each other.
  - Router: A networking device that forwards data packets between computer networks. They know where to send your packets on the internet.
    - Used to connect a local network to the internet or to connect multiple local networks together.
  - Switch: Takes a packet and send it to the correct server/client on your network.
    - Used to connect computers, printers, and other devices within a local area network (LAN).
- **Typical Network Path between different networks (internet):**
  - Client -> Switch -> Router -> Internet -> Router -> Switch -> Server/Client
- **Typical Network Path between same network:** Client -> Switch -> Server/Client

## Traditionally, how to build infrastructure:

- **On-premise:** Locally hosted computing infrastructure.
- Home: Your start point with some servers.
- Office with a Datacenter: Your company grows and you need more and better space for your servers.

  ## Problems with this approach:

  - Pay for the rent for the data center.
  - Pay for power supply, cooling, maintenance.
  - Adding and replacing hardware takes time.
  - Scaling is limited (space, etc..)
  - Hire 24/7 team to monitor the infrastructure
  - How to deal with disasters? (earthquake, power shutdown, fire...)

## Cloud computing: AWS owns and maintains everything, you just pay for on-demand compute power

- Is the on-demand delivery of compute power, database storage, applications and other IT resources.
- Through a cloud services platform with pay-as-you-go pricing.
  - pay-as-you-go: the same as you do with your electricity bill.
- Provision exactly the right type and size of computing resources you need.
- Access as many resources as you need, instantly.
- Simple way to access servers, storage, databases and a set of application services.

## The Deployment Models of the Cloud

- **Private Cloud:** Rackspace
  - Cloud services used by a single organization, not exposed to the public.
  - Complete control.
  - Security for sensitive applications.
  - Meet specific business needs.
- **Public Cloud:** (AWS, Azure, GCP)
  - Cloud resources owned and operated by a third party cloud service provider delivered over the internet.
  - Six Advantages of Cloud Computing (added below at this page)
- **Hybrid Cloud:**
  - Keep some servers on premises and extend some capabilities to the Cloud.
    - On AWS you can do that with [AWS Outposts](https://aws.amazon.com/outposts/).
  - Control over sensitive assets in your private infrastructure.
  - Flexibility and cost-effectiveness of the public cloud.

## Five characteristics of Cloud Computing

- **On-demand self service:**
  - Users can provision resources and use them without human interaction from the service provider
- **Broad network access:**
  - Resources available over the network, and can be accessed by diverse client platforms.
- **Multi-tenancy and resource pooling:**
  - Multiple customers can share the same infrastructure and applications with security and privacy.
  - Multiple customers are serviced from the same physical resources.
- **Rapid elasticity and scalability:**
  - Automatically and quickly aquire and dispose resources when needed.
  - Quickly and easily scale based on demand.
- **Measured service:**
  - Usage is measured, users pay correctly for what they have used.

## Six Advantages of Cloud Computing

- Trade capital expense (CAPEX) for operational expense (OPEX)
  - Pay On-Demand: don't own hardware
  - Reduced Total Cost of Ownership (TCO) & Operational Expense (OPEX)
- Benefit from massive economies of scale:
  - Prices are reduced as AWS is more efficient due to large scale.
- Stop guessing capacity: Scale based on actual measured usage.
- Increase speed and agility.
- Stop spending money running and maintaining data centers.
- Go global in minutes: leverage the AWS global infrastructure.

## Problems solved by the Cloud

- **Flexibility:** Change resource types when needed
- **Cost-Effectiveness:** Pay as you go, for what you use.
- **Scalability:** Accommodate larger loads by making hardware stronger or adding additional nodes.
- **Elasticity:** Ability to scale out and scale-in when needed.
- **High-availability and fault-tolerance:** build across data centers.
- **Agility:** Rapidly develop, test and launch software applications.

## Different types of Cloud computing

- **Infrastructure as a Service (IaaS):** (AWS EC2, VPC...)
  - Provide building blocks for cloud IT.
  - Provides networking, computers, data storage space.
  - Highest level of flexibility.
  - Easy parallel with traditional on-premises IT.
- **Platform as a Service (PaaS):** (AWS Lambda, Elastic Beanstalk, ECS, Amplify...)
  - Removes the need for your organization to manage the underlying infrastructure.
  - Focus on deployment and management of the application.
- **Software as a Service (SaaS):** (Gmail...)
  - Completed product that is run and managed by the service provider.

- **On-premise you need to manage:**
  - Applications, Data, Runtime, OS, Middleware, Virtualization, Servers, Storage, Networking.
- **IaaS:**
  - You need to manage: Applications, Data, Runtime, OS, Middleware.
  - Managed by others (AWS): Virtualization, Servers, Storage, Networking.
- **PaaS:**
  - You need to manage: Applications, Data.
  - Managed by others (AWS): Runtime, OS, Middleware, Virtualization, Servers, Storage, Networking.
- **SaaS:** Everything is managed by others.

## !Important
- **Advantages of Cloud**: Speed and Agility, stop guessing capacity.
