# AWS Account Management

## AWS Organizations - (Manage multiple AWS accounts centrally.)

- Groups of AWS accounts, can be nested.
- **MASTER ACCOUNT**: The management account, the one that have created the Organization.
- **Consolidated Billing** across all accounts.
- **Cost benefits**:
  - discounts because of aggregate usage, single payment method,
  - Pooling **EC2 Reserved Instances** for optimal savings
- API is available to automate AWS account creation.
- Restrict account privileges using Service Control Policies (SCP).

  ### Multi account strategies

  - Create accounts per department, per cost center, per dev/test/prod, compliance restrictions, etc...
  - Multi Account and One Account Multi VPC
  - Enable CloudTrail on all accounts, send logs to central S3 account.
  - Send CloudWatch Logs to central logging account.
  - Use **tagging** standards for billing purposes.

  ### Organizational UNITS (OU)

  - Business unit
  - Enivronmental LifeCycle
  - Project Based

## Service Control Policy (SCP)

- Whitelist or blacklist IAM actions.
- Applied at the **Organizational Unit** or **Account Level**.
- Does not apply to the Master account.
- SCP is applied to all **Users and Roles** of the Account, **including Root**.
- SCP are not applied to service roles.
- SCP must have an explicit allow (does not allow anything by default).
- **Use case example**:
  - Restrict access to certain services (example: "this account cannot use S3)

## AWS Control Tower - (multi-account AWS environment)

- Simplifies the setup and governance of a secure, compliant multi-account AWS environment.
- It runs on AWS Organizations, organizing accounts and implementing Service Control Policies (SCPs).
- **Benefits**:
  - **Automated Setup**: Quick environment setup.
  - **Policy Management**: Automated guardrails for policy management.
  - **Violation Detection**: Identify and remediate policy violations.
  - **Compliance Monitoring**: Track compliance via an interactive dashboard.

## AWS Resource Access Manager (AWS RAM) - (share your AWS resources with other AWS accounts)

- AWS RAM allows you to share AWS resources with other accounts, either individually or within your Organization.
- **Key Features**:
  - **Resource Sharing**: Share your resources to avoid duplication.
  - **Flexible Sharing**: Share with any AWS account or within your Organization.
  - **Supported Resources**: Includes Aurora, VPC Subnets, Transit Gateway, Route 53, EC2 Dedicated Hosts, License Manager Configurations, and more.

## AWS Service Catalog - (control what services can be used in an Organization)

- AWS Service Catalog helps new users navigate AWS options and launch compliant, pre-defined products.
- **Key Features**:
  - **Self-Service Portal**: Quick access to authorized products.
  - **Includes**: Virtual machines, databases, storage options, etc.

## Pricing Models in AWS

- AWS offers four pricing models:

  1. **Pay as You Go**: Pay for what you use; stay agile and responsive.
  2. **Save When You Reserve**: Reduce risks and manage budgets with reserved capacity (e.g., EC2, DynamoDB).
  3. **Pay Less by Using More**: Enjoy volume-based discounts.
  4. **Pay Less as AWS Grows**: Benefit from lower costs as usage increases.

  ### Free Services & Free Tier

  - **Free Services**: IAM, VPC, Consolidated Billing, Elastic Beanstalk, CloudFormation, Auto Scaling Groups (resource usage may incur costs).
  - **Free Tier**: Includes services like EC2 t2.micro for a year, S3, EBS, ELB, and AWS Data Transfer.

# Summary:

- AWS Account Management encompasses AWS Organizations for centralized control over multiple accounts, enabling consolidated billing and the use of Service Control Policies (SCP) to restrict access at the organizational unit or account level. AWS Control Tower facilitates the governance of multi-account environments with automated setups and compliance monitoring. The AWS Resource Access Manager allows resource sharing across accounts, promoting efficiency and cost savings. Additionally, AWS Service Catalog provides a self-service portal for launching compliant products. Lastly, AWS offers various pricing models, including pay-as-you-go and reserved capacity, along with free services and the Free Tier for new users.
