# AWS Cloud Monitoring

## Amazon CloudWatch Metrics

- Provide metrics for every services in AWS.
- Metric is a variable to monitor (CPUUtilization, NetworkIn).
- Metrics have timestamps.
- Can create a CloudWatch dashboard of metrics.

  - ### Important metrics
    - **EC2 instances**: CPU Utilization, Status Checks, Network (ram is not available)
    - **EBS Volumes**: Disk read/writes.
    - **S3 Buckets**: BucketSizeBytes, NumberOfObjects, AllRequests.
    - **Billing**: Total estimated charge (only in us-east-1)
    - **Service Limits**: How much you've been using a service API.
    - **Custom metrics**.

## Amazon CloudWatch Alarms

- Used to trigger notifications for any metric. -> When a metric achieve the threshold
- Alarms actions:
  - Auto Scaling: increase or decrease EC2 instances "desired" count.
  - EC2 Actions: stop, terminate, reboot or recover an EC2 instance.
  - SNS Notifications: send a notification into an SNS Topic if achieve some %.
- Various options for creating the alarm (%, max, min, etc..)
- Can choose the period on which to evaluate an alarm (1minute, 1h, etc..)
- Example: create a **billing alarm** on the CloudWatch billing metric. To notify if you achieve some $.

## Amazon CloudWatch Logs

- Can collect logs from:
  - Elastic Beanstalk from application.
  - ECS from containers.
  - AWS Lambda from function logs.
  - CloudTrail based on filter.
  - ClodWatch log agents: on EC2 machines or on-premises servers.
  - Route53: Log DNS queries.
- Enables real-time monitoring of logs.
- Adjustable CloudWatch Logs retention (1 year, weeks, months...)

  ### - CloudWatch Logs for EC2

  - By default no logs from EC2 will go to CloudWatch.
  - You need to create a CloudWatch Log agent on EC2 to push the log files you want.
  - You need to check the correct IAM permissions.

## Amazon Event Bridge (formerly CloudWatch Events)

- Schedule Cron jobs:
  - Every hour call a lambda service.
- Event pattern, to react a service doing something:
  - IAM Root Sign in Event -> SNS Topic with Email Notification
- Trigger Lambda, send sqs or sns messages, etc..
- Types of **Event Bus**:
  - **Default Event Bus (from AWS)**
  - **Partner Event Bus (from datadog...)**
  - **Custom Event Bus (your own custom apps)**
- Schema registry: Model event schema.
- You can archive events.
- Ability to replay archived events.

## AWS CloudTrail - see changes within your account
- Provides governance, compliance and audit for your AWS Account.
- CloudTrail is enabled by default.
- Get an history of events/API calls made within your AWS Account:
  - Console
  - SDK
  - CLI
  - AWS Services
- Can put logs from CloudTrail into CloudWatch Logs or S3.
- A trail can be applied to all Regions or a single Region.
- **Usage example**:
  - If a resource is deleted in AWS, investigate CloudTrail first!

## AWS X-Ray
- **Debugging in Production, the good old way**:
  - Test locally
  - Add log statements everywhere
  - Re-deploy in production
- Not so good because log formats differ across applications and log analysis is hard.
- Debugging: one big monolith "easy", distributed services "hard".
- **With AWS X-Ray**
  - Visual analysis of our applications.
  - Troubleshooting performance (bottlenecks).
  - Understand dependencies in a microservice architecture.
  - Pinpoint service issues.
  - Review request behavior.
  - Find errors and exceptions
  - Are we meeting time Service level agreement (SLA) - response time, etc..
  - Where am I throttled?
  - Identify users that are impacted.

## Amazon CodeGuru
- An ML-powered service for automated code reviews and application performance recommendations.
  - **CodeGuru Reviewer**: Automated code reviews for static code analysis (development).
    - find vulnerabilities, resource leaks, bugs.
    - Integrates with Github, Bitbucket, and AWS CodeCommit.
  - **CodeGuru Profiler** visibility/recommendations about application performance during runtime (production).
    - identify if your application is consuming excessive CPU capacity.

## AWS Health Dashboard

  ### - Service History: - general status of all AWS Services
    - Shows all regions, all services health.
    - Shows historical information for each day.
    - Has an RSS (brief introduction) feed you can subscribe to.
    - Previously called AWS Service Health Dahsboard.

  ### - Your account - status of AWS services of your account resources
    - Provides alerts (notifications) and remediation guidance when AWS is experiencing events that may impact you.
    - AWS outages directly impact you.

## !Important
- Alerts = CloudWatch. (except for **AWS Budgets** that is monitoring costs)
  - For example, how to know if your aws root account is being used? **CloudWatch + CloudTrail sign-in alerts**
  - **CloudWatch** primarily monitors **performance metrics** for AWS resources (e.g., CPU, memory, logs, etc.) and can generate **alerts based on those metrics**.
  - **AWS Budgets** is the service **specifically** used for **cost monitoring** and setting **spending alerts**.
- **AWS X-Ray**: monitor and debug distributed applications by providing insights into performance, request tracing, and error detection. --> you can check end-to-end user requests made in the applications