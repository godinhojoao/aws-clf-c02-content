# AWS IAM - Identity & Access Management (Global Service)

## When to use IAM?

- Sharing your AWS account with others, for example, if you are a entrepeneur you probably need that your developers access specific resources on your AWS account without having your admin credentials.
- To control and secure the access to your critial AWS Resources.
- IAM allows you to assign **granular permissions**. In this way you can control the exactly actions that each user can do on your AWS environment.
  - You can allow some users to just read specific resources.
  - Allow just some actions in a resource, etc.
- Improving security: Multi-Factor Authentication (MFA), to your account and to individual users.

## [When IAM is used for each job function](https://docs.aws.amazon.com/IAM/latest/UserGuide/when-to-use-iam.html):

- **Service user**: If you use an AWS service to do your job, then your administrator provides you with the credentials and permissions that you need. As you use more advanced features to do your work, you might need additional permissions. Understanding how access is managed can help you request the right permissions from your administrator.

- **Service administrator**: If you're in charge of an AWS resource at your company, you probably have full access to IAM. It's your job to determine which IAM features and resources your service users should access. You must then submit requests to your IAM administrator to change the permissions of your service users. Review the information on this page to understand the basic concepts of IAM.

- **IAM administrator**: If you're an IAM administrator, you manage IAM identities and write policies to manage access to IAM.

## Identity based policies "What resources this (user, group, role) can access?"

- ## Users & Groups

  - On AWS, a **Root Account** is created by default. You should use this account to create a user and then avoid using the Root Account for regular tasks.
  - **Groups**: Used to grant specific **policies** (permissions) to the users that are inside the group.
  - **Users**: People within your organization, that can be grouped together.
    - For example, group called "developers", that can do specific stuff on AWS.
    - One user can have more than one group.
    - One user can have the policy directly without having a group, but this is not a good practice.

  - ## How to configure IAM Policies and IAM Groups?
  - You can do that by the `IAM Policy JSON` that's used to describe permissions within AWS.

  Example of the structure of IAM policies:
  ```JSON
  {
    "Version": "2024-07-24",
    "Id":  "S3-Account-Permissions",
    "Statement": [
      {
        "Sid": "1", // statement id (optional)
        "Effect": "Allow", // Allow | Deny
        "Action": [ // Which tasks are allowed
          "s3:DeleteObject",
          "s3:GetObject",
          "s3:*",
        ],
        "Condition": { // Conditions that need to be met for authorization (optional)
          "IpAddress": {
            "aws:SourceIP": "10.14.8.0/24"
          }
        },
        "Resource": [ // Resources
          "arn:aws:s3:::example_bucket" // Amazon resource name (ARN), an unique name that identify aws resources
        ]
      }
    ]
  }
  ```

- ## You can bring your company employees to AWS IAM in 3 steps:

  - 1. Create Groups
  - 2. Attach AWS Policies to these groups
  - 2. Add the users in the respective group

- ## IAM Roles

  - It's similar to an IAM user, in which you can attach policies with permissions. You can attach this role to any user/resource that you need.
  - Use cases:
    - You have an AWS EC2 instance that needs to access an AWS S3 bucket, but instead of adding your credentials within the code you can attach an IAM Role to your EC2 instance.
    - You can use IAM roles to attach specific permissions temporarily for your users when needed. For example, if an specific developer needs to manage an AWS S3 Bucket. After fixing what needed you can remove the role of this user and then he will return with his correct permissions.

## Resource Based Policies "Who can access this resource?"

- We already talked about Identity Based Policies, for users, groups and roles.
- Now let's discuss about Resource Based Policies, in which you can define the permissions inside the resource itself.
- For example, if you want to define that a specific user can perform actions inside a Amazon S3 bucket, you can define it within the Amazon S3 Bucket directly.

Example of the structure of resource based policies:
```JSON
{
  "Version": "2024-07-24",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { // Who is receiving access to the resource
        "AWS": "arn:aws:iam::123456789012:user/ExampleUser"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example_bucket/*"
    }
  ]
}
```
## How can you access AWS?
- Main options
  - AWS Management Console - web: protected with password and MFA
  - AWS Command Line Interface - CLI: protected by access keys
    - User on CLI has the same access than the web console, configured on IAM.
  - AWS Cloud Shell: A terminal in the AWS cloud that you can access through the AWS Management Console. (CLI on console)
  - AWS Software Developer Kit - SDK: protected by access keys
    - Enables you to access AWS services and use them within your application code.
    - Set of Libraries. Language-specific APIs.
- Each user manage it's own access key, and access keys are secret just like passwords.
- Where to generate a AWS Access Key?
  - On AWS Console inside the IAM service you need to generate an access key by a specific user.

## Security

- ## IAM Password Policy
  - You can define a password policy to your account, in this way all users will be required to follow this password rule.
    - Require specific length of letters, uppercase, lowercase, numbers, etc...
  - You can also define a password expiration time in which the users would need to create a new password after this expiration time.
  - Prevent password reuse.

- ## Multi Factor Authentication - MFA
  - You can require users within your AWS account to configure MFA for better security in case of leaked password.

- ## IAM Tools
  - **IAM Credentials Report (account-level)**
    - Report that lists all your account's users and the status of their credentials.
  - **IAM Access Advisor (user-level)**
    - Show the service permitions granted to a user and when those services were last accessed.
    - You can use this information to revise your policies.
    - You will see that the user is just using some services and you don't need to grant full permissions for this user.

## IAM Best practices
- Don't use root account, except for AWS account setup.
- One physical user = one aws user.
- Assign users to groups and permissions to groups.
- Create a strong password policy.
- Use and enforce MFA.
- Create and use IAM Roles for giving permissions to AWS Services.
- Use Access Keys for Programmatic Access (CLI/SDK).
- Never share IAM users and Access keys.

## Important!
- **Principal** Who is authorized to access something. (IAM user, root user, role, application, etc..)

## Shared responsibility Model for IAM
- AWS -> security OF the cloud: infrastructure (global network), vulnerability analysis, compliance validation.
- USER -> security IN the cloud:
  - Managing account, creating groups, users, roles and access keys correctly.
  - Enabling MFA on all accounts.
  - Rotate your access keys and credentials often.
  - Using IAM tools to apply appropriate permissions.
  - Analyze access patterns to review permissions. (IAM Credentials Report and Access Advisor)

## Reference

- https://docs.aws.amazon.com/iam/index.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-iam-features.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/when-to-use-iam.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-managing-iam.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html
