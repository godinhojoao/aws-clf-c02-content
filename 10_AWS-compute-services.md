# AWS Compute services (summary)

## Amazon ECS - Elastic Container Service
- Basically a orchestration service to launch docker containers.
- You still need to provision and maintain the infrastructure (EC2 instances).
- **Fargate**:
  - Same thing but now you don't need to provision the EC2 instances, because fargate will be running everything serverless.
  - In this way you can focus on the business/application and forget the infrastructure.

## Amazon ECR - Elastic Container Registry
- Private Docker Registry that is used to store docker images on AWS.
- These docker imagens can be run by ECS or Fargate.

## What's Serverless?
- A new paradigm in which the developers don't have to manage servers anymore. They just deploy code or functions.
- Serverless doesn't means there are no servers, it means that you just don't manage/ provision / see them.
- **Initially**: Serverless == FaaS (Function as a Service)
- Serverless was pioneered by AWS Lambda but now also includes anything that's managed:
  - databases, messaging, storage, etc...
- **Examples**:
  - DynamoDB -> We just use the tables without provision any server for that. AWS is doing it in the back.
  - S3 -> We just create a bucket and upload files there. AWS is provisioning servers in the back.
  - Fargate -> We just select the containers we need to run. AWS is provisioning the servers.

## AWS Lambda
- Virtual functions, no servers to manage.
- Limited by time, short executions.
- Run on-demand. (not running countinuosly as an EC2 Instance)
- Scalling is automated.
- **Benefits**:
  - Easy pricing, pay for request and compute time.
  - Great for short executions, and integrated with the whole AWS services
  - Event-Driven: If you receive an event and need to handle it, use AWS Lambda.
- **Example**: Thumbnail creation service
  - 1st step: New image in S3 triggers an event
  - 2nd step: AWS lambda function creates a thumbnail and uploads on S3 and also saves metadata of the thumbnail on DynamoDB.

## Amazon API Gateway -> Building Serverless APIs
- Imagine that you have a Lambda function that is doing a CRUD on DynamoDB.
- But you need your clients (frontend) using this lambda function as an API.
- To do that you can expose it using an **API Gateway** to proxy the request to AWS Lambda.

## AWS Batch
- Fully managed batch processing at **any scale**.
- A batch job is a job with a start and an end (opposed to continuous). Example: from 1am to 3am
- Batch will dynamically launch EC2 instances or Spot Instances.
- AWS Batch provisions the right amount of compute/memory.
- You submit or schedule batch jobs and AWS Batch does the rest.
- Batch jobs are defined as Docker images and run on ECS.
- **AWS Batch vs AWS Lambda**
  - Batch: No time limit, any runtime because it's packaged on docker, rely on EBS/ Instance store, relies on EC2.
  - Lambda: Time limit, limited runtimes, limited temporary disk space, serverless.

## AWS Lightsail -> If you are starting on the cloud and need to create an entire simple application
- Virtual servers, storage, databases, and networking
- Low and predictable pricing
- Simpler alternative to using EC2, RDS, ELB, EBS, etc..
- Great for people with little cloud experience.
- Can setup notifications and monitoring of your Lightsail resources.
- **Use cases**: Simple web applications and Websites.
- Has high availability but no auto-scaling, limited AWS integrations.

## !Important
- **Lambda && AWS Fargate**: Serverless Computing Services.

## Reference

- https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html
- https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html
- https://docs.aws.amazon.com/lambda/latest/dg/welcome.html
- https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html
- https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html
- https://docs.aws.amazon.com/lightsail/latest/userguide/what-is-amazon-lightsail.html