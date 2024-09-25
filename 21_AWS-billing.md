# AWS Billing

## Compute Pricing – EC2

- **Pay for What You Use**: Charges based on instance configuration, region, OS, and monitoring.
- **On-Demand Instances**:
  - Minimum charge of 60 seconds.
  - Pay per second (Linux/Windows) or per hour (other).
- **Reserved Instances**:
  - Up to 75% discount on hourly rates with 1- or 3-year commitment.
  - Options for all upfront, partial upfront, or no upfront payment.
- **Spot Instances**:
  - Up to 90% discount; bid for unused capacity.
- **Dedicated Hosts**:
  - On-demand or 1- or 3-year reservations.
- **Savings Plans**: Alternative for savings on sustained usage.

## Compute Pricing – Lambda & ECS

- **Lambda**:
  - **Pay Per Call**: Charges based on the number of requests.
  - **Pay Per Duration**: Costs calculated by the execution duration.
- **ECS**:
  - **EC2 Launch Type**: No additional fees; pay for AWS resources used in your application.
  - **Fargate Launch Type**: Pay for vCPU and memory resources allocated to your containerized applications.

## Storage Pricing – S3

- **Storage Classes**: S3 Standard, Infrequent Access, Glacier, etc.
- **Pricing Factors**:
  - Object number/size (tiered pricing).
  - Requests and data transfer out.
  - S3 Transfer Acceleration and lifecycle transitions.

## Storage Pricing – EBS

- **Volume Type**: Based on performance.
- **Charges**:
  - Per GB per month provisioned.
  - IOPS (General Purpose SSD included; others based on provisioned amount).
  - Snapshots per GB per month.
  - Outbound data transfer tiered; inbound is free.

## Database Pricing – RDS

- **Billing**: Per hour.
- **Factors**: Engine, size, memory class.
- **Purchase Types**: On-demand or Reserved Instances (1/3 years).
- **Charges**: Additional storage and I/O requests per month; free inbound data transfer.

## Content Delivery – CloudFront

- **Pricing**: Varies by region.
- **Charges**: Data transfer out (volume discounts) and HTTP/HTTPS requests.

## Networking Costs in AWS per GB

- **Traffic Costs**:

  - **In**: Free.
  - **Private IP**: Free.
  - **Public IP / Elastic IP**: $0.02.
  - **Inter-region**: $0.02.

- **Best Practices**:
  - Use **Private IP** for savings.
  - Stay in the **same Availability Zone** for cost savings.

## Savings Plan

- Commit to a $ amount per hour for 1 or 3 years.
- **Types**:
  - **EC2 Savings Plan**: Up to 72% off On-Demand.
  - **Compute Savings Plan**: Up to 66% off, flexible usage.
  - **Machine Learning Savings Plan**: For SageMaker.
- **Setup**: Via AWS Cost Explorer.

## AWS Compute Optimizer

- Optimize AWS resources to reduce costs and improve performance.
- **Features**:
  - Analyzes configurations and utilization with Machine Learning.
  - Right-sizes workloads (over/under provisioned).
- **Resources**: EC2 instances, Auto Scaling Groups, EBS volumes, Lambda functions.
- **Savings**: Up to 25% cost reduction.
- **Export**: Recommendations can be exported to S3.

## Billing and Costing Tools

- **AWS Pricing Calculator**: Estimate costs for solution architectures at [calculator.aws](https://calculator.aws/).
- **AWS Billing Dashboard**: Monitor billing details.
- **AWS Free Tier Dashboard**: Track usage of free tier services.

### Cost Allocation Tags

- **Purpose**: Track AWS costs in detail.
- **Types**:
  - **AWS-Generated Tags**: Automatically applied, prefixed with `aws:` (e.g., `aws:createdBy`).
  - **User-Defined Tags**: Custom tags created by users, prefixed with `user:`.

### Tagging and Resource Groups

- **Usage**: Organize resources like EC2, RDS, VPC, and IAM.
- **Resource Groups**: Create collections of resources based on shared tags.
- **Tag Management**: Use the Tag Editor for managing tags.

## Cost and Usage Reports

- **Purpose**: Analyze AWS costs and usage in detail.
- **Content**: Comprehensive data on costs, usage, and metadata for AWS services (e.g., EC2 RIs).
- **Details**: Lists usage by service in hourly/daily line items, including activated cost allocation tags.
- **Integration**: Compatible with Athena, Redshift, and QuickSight.

## Cost Explorer

- **Purpose**: Visualize and manage AWS costs and usage over time.
- **Features**:
  - Create custom reports for detailed analysis (monthly, hourly, resource level).
  - Optimize savings with Savings Plans.
  - Forecast usage for up to 12 months based on historical data.

## Billing Alarms

- **Functionality**: Monitor billing data through CloudWatch (us-east-1).
- **Scope**: Reflects actual worldwide AWS costs, not projected.
- **Alarm Type**: Basic alerts (less complex than AWS Budgets).

## AWS Budgets

- **Function**: Create budgets and receive alerts when costs exceed limits.
- **Types**: Usage, Cost, Reservation, Savings Plans.
- **Reserved Instances**: Track utilization for EC2, ElastiCache, RDS, Redshift.
- **Notifications**: Up to 5 SNS alerts per budget.
- **Filters**: Service, Linked Account, Tag, etc.
- **Cost**: First 2 budgets free, then $0.02 per additional budget per month.

## AWS Cost Anomaly Detection

- **Purpose**: Monitor costs using ML to detect unusual spending patterns.
- **Functionality**:
  - No thresholds needed; learns historical spending.
  - Monitor services, accounts, tags, or categories.
  - Provides reports with root-cause analysis.
  - Alerts via SNS.

## AWS Service Quotas

- **Function**: Notify when approaching service quota thresholds.
- **Integration**: Create CloudWatch alarms.
- **Example**: Lambda concurrent executions.
- **Action**: Request quota increases or manage resources proactively.

## Trusted Advisor

- **Function**: Provides account assessments without installation.
- **Categories**: Cost optimization, Performance, Security, Fault tolerance, Service limits, Operational Excellence.
- **Access**: Full checks available with Business & Enterprise Support plans.

## AWS Support Plans

1. **Basic Support**: Free access to customer service, Trusted Advisor (7 checks), and Health Dashboard.
2. **Developer Support**: All Basic features + email access to Cloud Support during business hours, unlimited cases.
3. **Business Support**: 24/7 access to support, full Trusted Advisor checks, unlimited cases, and faster response times.
4. **Enterprise On-Ramp Support**: All Business features + access to Technical Account Managers (TAMs) and additional support options.
5. **Enterprise Support**: All Business features + dedicated TAM and concierge support for critical workloads.

# Summary:
- The AWS billing framework includes various pricing models, such as On-Demand, Reserved, and Spot Instances for EC2, alongside pay-per-use options for Lambda and ECS. Key storage options include tiered pricing for S3 and performance-based pricing for EBS. Tools like the AWS Pricing Calculator, Billing Dashboard, and Cost Explorer help monitor and manage costs effectively. Additionally, features like cost anomaly detection and tagging enhance cost tracking, while AWS support plans offer tailored assistance for resource optimization.
