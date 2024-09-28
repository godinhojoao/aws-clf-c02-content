# AWS Advanced Identity

## AWS STS - Security Token Service

- Create temporary security credentials with limited privileges to access your AWS resources.
- These credentials are short-term and come with an expiration time.
- **Usage example**:
  - A user or application can assume a role using AWS STS to gain temporary credentials.
  - After the expiration time, the credentials will no longer be valid, and the user or application will lose access to the associated AWS resources.
- **Use cases**:
  - **Identity federation**: manage user identities in external systems, and provide them with STS tokens to access AWS resources.
  - **IAM Roles cross/same account access**
  - **IAM Roles for Amazon EC2**: provide temporary credentials for EC2 instances to access AWS resources.

## Amazon Cognito

- Identity for Web and Mobile Applications. (for potentially millions of users).
- **User Management**: Instead of creating IAM users for each application user, create users in Cognito.
- Simplifies user sign-up, sign-in, and access control.
- **Example**:
  - You have a database of user information.
  - Use Cognito to authenticate users, allowing them to sign in via social identity providers (like Google, Facebook) or via email/password.
  - After authentication, Cognito issues tokens (JWT) to access your backend services securely.

## AWS Directory services - (The same idea as Microsoft Active Directory)

- Provides a scalable directory service for user and resource management, similar to Microsoft Active Directory.
- Facilitates hybrid cloud scenarios by enabling integration with on-premises Active Directory, allowing organizations to extend their existing directory services to the cloud.

## AWS IAM Identity Center - (Successor to AWS Single Sing-on)

- SSO is an authentication process that **allows users to access multiple applications with a single set of login credentials** (username and password).
- **One login (single sign-on) for all your:**
  - AWS accounts in AWS Organizations
  - Business cloud applications (ex: salesforce, microsoft 365...)
  - EC2 Windows Instances
- **Identity Providers: (where user data is stored)**
  - Built-in identity store in IAM Identity Center.
  - 3rd party: Active Directory, OneLogin...
- **Example of usage**:
  - You log in at a specific URL -> access the AWS IAM Identity Center portal -> view the AWS accounts you have access to using these credentials -> choose an account and perform the necessary tasks.

## !Important
- **AWS IAM Identity Center**: Provides SSO on aws account - single sign on.
- **Amazon Cognito**: Provides social login for your web and mobile applications.
- **Federated Identities**: allow users to authenticate with external identity providers and access AWS resources using temporary credentials. -> use case **if your company merges with another one and new employees need to access aws resources.**