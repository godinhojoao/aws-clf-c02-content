## AWS Scalability

- Means that an apllication can handle greater loads by adapting.
- Or making the hardware stronger (scale up) or by adding more nodes (scale out).
  - **Vertical**: scale up or down
    - Increase the size of an instance (+ compute power).
    - Good option for non distributed systems like a database.
  - **Horizontal (= elasticity)**: scale out or in
    - Increase the number of instances/systems for your application.
    - Good option for distributed systems.
    - Auto Scaling Group & Elastic Load Balancing

## High Availability

- Means running your application/system in at least 2 Availability Zones (AZ).
  - Auto Scaling Group multi AZ & Load Balancer multi AZ
- The idea is to survive a data center loss (disaster).
- Usually goes hand in hand with horizontal scaling.

## AWS ELB - Elastic Load Balancing

- First what are **Load Balancers**?
  - Load balancers are servers that forward internet traffic to multiple servers (EC2 instances) downstream.
  - **Usecases**:
    - Spread load across downstream instances.
    - Expose a single point of access (DNS) to your application.
    - Seamlessly handle failures of downstream instances.
    - Do regular health checks to your instances.
    - Provide SSL termination (HTTPS) for your websites.
    - High availability across zones.
- **AWS ELB - Elastic Load Balancing** is a **managed load balancer of AWS**.

  - AWS takes care of upgrades, maintenance, high availability and provides a few configurations.
  - It costs more but saves you a lot of time compared to creating and maintaining a load balancer yourself.

- ## Application Load Balancer - ALB

  - HTTP / HTTPs / gRPC protocols (Layer 7)
  - HTTP routing features
  - Static DNS (URL)
  - Users sends http/https/grpc traffic to the application load balancer and it route traffic to your servers (EC2 instances).

- ## Network Load Balancer - NLB

  - TCP/UDP protocols (Layer 4)
  - High Performance: millions of requests per second.
  - Static IP through Elastic IP
  - Users sends TCP/UPD traffic to the Network load balancer and it route traffic to your servers (EC2 instances).

- ## Gateway Load Balancer - GWLB
  - GENEVE Protocol on IP Packets (Layer 3)
  - Route Traffic to Firewalls that you manage on EC2 instances.
  - Intrusion detection
  - Users sends IP packets to our Gateway load balancer, it is analyzed (security) and then goes to the application (EC2 instances).

## AWS ASG - Auto Scaling Group

- In real-life, the load on your websites and applications can change in specific days and periods.
- The purpose of an Auto Scaling Group is: **ELASTICITY**:
  - **Scale OUT**: (ADD EC2 instances) to match an increased load.
  - **Scale IN**: (REMOVE EC2 instances) to match an decreased load.
  - Ensure we have a min and max number of machines running.
  - Automatically register new instances to a load balancer.
  - Replace unhealthy instances, terminate and replace for a new one.
- Cost Savings: only run at an ideal capacity.

- ## Auto Scaling Group Strategies
- **Manual Scaling**: Update the size of an ASG manually
- **Dynamic Scaling**: Respond to changing demand
  - Simple/Step Scaling: When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 instances. Or CPU < 30%, remove 2 instances.
  - Target Tracking Scaling: I want the average ASG CPU to stay at around 40%.
  - Scheduled Scaling: Anticipate a scaling based on known usage patterns. Example: increase minimum capacity on fridays at 5pm.
- **Predictive Scaling**: Uses machine learning to predict future traffic ahead of time.
  - Automatically provisions the right number of EC2 instances in advance.

## !Important

- **Elastic Load Balancer**: is an example of elasticity principle.
- **Application Load Balancer (ALB)**: Routes HTTP/HTTPS/gRPC traffic to EC2 instances using Layer 7 features.
  - Example: Communicate with ports 80 (HTTP) and 443 (HTTPS).
  - **Use Case**: Load balancing web applications with URL-based routing.
- **Network Load Balancer (NLB)**: Distributes high-performance TCP/UDP traffic to EC2 instances with Layer 4 capabilities.
  - Example: Handle millions of requests per second for gaming or IoT applications.
- **Gateway Load Balancer (GWLB)**: Analyzes IP packets with the GENEVE protocol for security before routing to EC2 instances.
  - Example: Routing traffic to firewalls for intrusion detection.
- **Classic Load Balancer (CLB)**: Legacy applications.

## Reference

- https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/auto-scaling-groups.html
