# AWS VPC and Networking

## What AWS requires you to know about VPC for Cloud Practicioner exam:
- VPC, Subnets, Internet Gateways and NAT Gateways
- Security Groups, Network ACL (NACL), VPC Flow Logs
- VPC Peering, VPC Endpoints
- Site to Site VPN and Direct Connect
- Transit Gateway

## Ip Addresses in AWS
- **IPV4 - Internet Protocl version 4 (4.3 Billion Addresses)**
  - **Public IPV4** - can be used on the internet
    - EC2 instance gets a new public IP address every time you stop then start it (default)
  - **Private IPV4** - can be used on private netwroks (LAN) such as internal AWS networking (e.g 192.168.1.1)
    - Is fixed for EC2 instance even if you start/stop them.
  - **AWS Elastic IP** - Allows you to attach a fixed public IPV4 address to EC2 instance.
  - **Pricing for all public IPV4**: $0.005 per hour (including EIP)
    - Free tier 750 hours usage per month.
- **IPV6 - Internet Protocl version 6 (3.4 * 10^38 Addresses)**
  - Every IP address is public in AWS (no private range)
  - Example: 2001:0000:130F:0000:0000:09C0:876A:130B
  - Free

## VPC - Virtual Private Cloud
- Private network to deploy your resources (Region resource on AWS).

  - ### Subnets - partition the network inside the VPC
    - Allow you to **partition your network inside your VPC** (Availability Zone resource on AWS)
    - A **public Subnet**: is a subnet that is accessible from the internet.
      - Things that need to be accessed from the internet, example: **EC2 instances**.
    - A **private Subnet**: not accessible from the internet.
      - Things that don't need to be accessed from the internet, example: **Databases**
    - To define access to the internet and between subnets, we use **Route Tables**.

  - ### VPC diagram on AWS
    - <img src="https://docs.aws.amazon.com/images/vpc/latest/userguide/images/subnet-diagram.png">
    - Region -> Availability Zone -> VPC -> Subnets

## Internet Gateway and NAT Gateways
- **Internet Gateway**: helps our VPC instances to connect with the internet.
- Public Subnets have a route to the Internet Gateway.
  - Internet Gateway <-> Public Subnet
- **NAT Gateways (AWS-Managed) and NAT Instances (self-managed)**
  - Allow your instances in your **Private Subnets** to access the internet while ramaining private.

## Network ACL and Security Groups

  - ### Network ACL - Access Control List -> SUBNET LEVEL
    - A firewall which **controlls traffic FROM and TO Subnet**.
    - Can have ALLOW and DENY rules.
    - Are attached at the Subnet level.
    - Rules only includes IP addresses.

  - ### Security Groups -> INSTANCE LEVEL
    - A firewall which **controls traffic FROM and TO an EC2**.
    - Can have only ALLOW rules.
    - Rules include IP Address and other security groups.

## VPC Flow Logs
- Capture information about IP traffic going into your interfaces.
  - VPC Flow Logs
  - Subnet Flow Logs
  - Elastic Network Interface Flow Logs
- **Helps to monitor and Troubleshoot connectivity issues**. Example:
  - Subnets to internet
  - Subnets to subnets
  - Internet to subnets
- VPC Flow Logs can go to S3, CloudWatch Logs, and Kinesis Data Firehose

## VPC Peering
- **Connect two or more VPCs**, privately using AWS network.
- **Make them behave as if they were in the same network.**
- Must not have overlapping CIDR (IP address range)
- VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another).
  - If you have a VPC Peering between: A -> B
  - And also a VPC Peering between: A -> C
  - You still need to create one between: B -> C

## VPC Endpoints -> connect to AWS services using private network
- Endpoints allow you to **connect to AWS Services using a private network** instead of the public www network.
- This gives you enhanced security and lower lattency access to AWS Services.
- **Inside a Private Subnet**
  - if you want to connect on **S3 or Lambda** --> **VPC Endpoint Gateway**
  - connect all others --> **VPC Endpoint Interface**

## AWS PrivateLink (VPC Endpoint Services)
- Most secure and scalable way to expose a service to 1000s of VPCs.
- Don't require: VPC Peering, internet gateway, NAT, route tables...
- <img src="https://docs.aws.amazon.com/images/vpc/latest/privatelink/images/use-cases.png">

## Site to Site VPN and Direct Connect

  - ### Site to Site VPN
    - Connect an on-premises VPN to AWS.
    - The connection is automatically encrypted.
    - Goes over the **public internet**.
    - Example: <img src="https://docs.aws.amazon.com/images/vpn/latest/s2svpn/images/vpn-how-it-works-vgw.png">
    - You need a **Customer Gateway** and a **Virtual Private Gateway**.
  - ### Direct Connect (DX) -> private network connection from on-premise to AWS
    - Physical connection between on-premises and AWS.
    - The connection is private, secure and fast.
    - Goes over a **private network**.
    - Take at least one month. But is much safer.

## AWS Client VPN
- Connect **from your computer** using OpenVPN **to your private network in AWS** and on-premises.
- Allow you to connect to your EC2 Instances over a Private IP (just as if you were in the private VPC network)
- Goes over the **public internet**.

## Amazon Transit Gateway
- The way AWS provides to connect thousands of VPCs together, on AWS cloud but also with on-premise infrastructure.
- One single Gateway to provide this functionality, works with Direct Connect, VPC Gateway, VPN connections...