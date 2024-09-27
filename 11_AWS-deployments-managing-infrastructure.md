# AWS Deployments and Managing Infrastructure at Scale

## CloudFormation - "Automate" The Setup of Infrastructure and Services

- Is a declarative way of outlining your AWS infrastructure, for any resources (most of them are supported).
- For example, within a CloudFormation template, you say:
  - I want a security group.
  - I want two EC2 instances using this security group.
  - I want a S3 bucket.
  - I want a load balancer ELB in front of these machines.
- Then CloudFormation creates those for you, in the **right order**, with the exact configuration that you specify.

  - ### Benefits of CloudFormation (Infrastructure as code)

    - No resources are manually created, which is good for control.
    - Changes to infrastructure are reviewed through code.
    - Productivity: Ability to destroy and re-create an infrastructure on the cloud on the fly.
    - Documentation: Automated generation of Diagram for your templates.
    - Declarative programming (no need to figure out ordering and orchestration)
    - Don't reinvent the wheel: Use existing templates on the web.
    - **Costs**:
      - Each resource has an identifier in which you can see the costs.
      - You can use a CloudFormation template to estimate your resource's costs.
      - Saving strategy: In Dev, you could automation deletion of templates at 5PM and recreated at 8am, safely.
    - You can basically create **templates** that are declarations of AWS resources that make up a stack.

  - ### CloudFormation + Application Composer
    - Application Composer is used to visualize the AWS CloudFormation template.
    - We can see all the resources and the relations between the components.

## AWS CDK - Cloud Development Kit

- Develop your cloud infrastructure using a programming language: java, javascript, python, etc..
- The code is "compiled" into a CloudFormation template (JSON/YAML)

## AWS Elastic Beanstalk (PaaS - Platform as a Service) -> focus on the code

- A developer centric view of deploying an application on AWS.
- It uses all the components we've seen before. (EC2, ASG, ELB, RDS, etc...)
- We still have control over the configuration but it's all in one view that's easy to understand.

  ### - Shared Responsibility Model on Elastic Beanstalk

  - **Beanstalk is responsible for**:
    - Instance configuration / OS.
    - Deployment strategy is configurable but performed by beanstalk.
    - Capacity provisioning.
    - Load balancing and auto-scaling.
    - Application health-monitoring and responsiveness.
  - **User is responsible for**: Application code.

  ### - Three architectures models:

  - Single Instance deploymend: dev environment.
  - LB + ASG: great for production or pre-production web applications.
  - ASG only: great for non-web apps in productions (workers, etc...)

## AWS CodeDeploy

- We want to deploy our application automatically.
- Works with: EC2 Instances, On-Premises Servers. It's called a **hybrid service** because of that.
- Servers/Instances must be provisioned and configured ahead of time with the CodeDeploy Agent.

## AWS CodeCommit (deprecated)
- The same as github, a remote repository to store your code.

### AWS CodeBuild
- Allows you to build a service in the cloud.
- It means:
  - Compiles source code -> run tests -> produces Artifact packages that are ready to be deployed for AWS CodeDeploy
- Pay as you go pricing, only pay for build time.

### AWS CodePipeline
- Orchestrate the different steps to have the code automatically pushed to production:
  - Code -> Build -> Test -> Provision -> Deploy
  - Basis for CI/CD
- Benefits:
  - Fully managed and compatible with CodeBuild, CodeDeploy, Elastic Beanstalk, CloudFormation, github, and more.
  - Fast delivery and rapid updates.

## AWS CodeStar
- Simplifies setting up, managing, and collaborating on software development projects using AWS services.

## AWS CodeArtifact
- Can be used to manage the dependencies (packages) of your application. For example the node_modules with npm.
- Stores and retrieve these dependencies is called **artifact management**.
- Developers and CodeBuild can retrieve dependencies directly from CodeArtifact.
- It can be also used to store different versions of an application dependencies.

## AWS SSM - Systems Manager
- Helps you manage EC2 and On-Premises systems at scale. It's called a **hybrid service** because of that.
- Get operational insights about the state of your infrastructure.
- Works for Linux, Windows, MacOS, and more...
- **Most important features**:
  - Patching automation for enhanced compliance.
  - Run commands across an entire fleet of servers.
  - Store parameter configuration with the SSM Parameter Store.
- **How it works?**
  - We need to install the SSM agent onto the systems we control. (installed by default by Amazon Linux AMI)

  - ### AWS System Manager (SSM) Session Manager -> connect on EC2 instance shell without SSH
    - Allows you to start a secure shell on your EC2 and on-premises servers.
    - No SSH access, bastion hosts, or SSH keys needed.
    - No port 22 SSH needed (better security)
    - Send session log data to S3 or CloudWatch Logs.

  - ### AWS System Manager (SSM) Parameters Store
    - Secure store for configurations, secrets, API Keys, etc...
    - It is serverless, you don't need to provision servers.
    - Control access permissions using IAM.
    - Version tracking & encryption (optional) using AWS KMS - Key management Service.

## Remember: CloudFormation and Elastic Beanstalk are free of use.

## !Important
- **AWS CloudFormation**: templates, that you can replicate across regions
- **AWS SSM Session Manager**: connect on EC2 instance shell without SSH, without opening new ports.

## Reference

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cloudformation.html
- https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html
- https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html
- https://docs.aws.amazon.com/codecommit/latest/userguide/welcome.html -> deprecated
- https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html
- https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html
- https://docs.aws.amazon.com/codeartifact/latest/ug/welcome.html
- https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html
