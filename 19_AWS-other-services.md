# AWS Other Services for CLF-C02

- Just a quick summary

## WorkSpaces - (DESKTOP as a service)

- Amazon WorkSpaces is a managed, secure Desktop-as-a-Service (DaaS) solution that allows users to provision Windows or Linux desktops in the cloud. It simplifies desktop management and provides users with access to their desktop environments from anywhere.

## AppStream 2.0 - (Stream an application to any computer in the cloud - you could play a game on cloud)

- Amazon AppStream 2.0 is a fully managed application streaming service that allows you to deliver desktop applications to users via a web browser. It enables you to stream applications securely without the need for infrastructure management.

## IoT Core - (easily connect IoT devices to AWS - billions)

- AWS IoT Core is a managed cloud service that enables connected devices to interact with cloud applications and other devices securely. It supports device connectivity, messaging, and data processing, making it easier to build IoT applications.

## Elastic Transcoder - (convert media files stored in S3 to required formats by consumer playback)

- AWS Elastic Transcoder is a cloud-based media transcoding service that allows you to convert media files into different formats. It simplifies the process of preparing video and audio content for playback on various devices.

## AppSync - (uses GraphQL to simplify application development and provide real-time data synchronization for mobile and web)

- AWS AppSync is a managed service that simplifies application development by providing a flexible GraphQL API. It enables real-time data synchronization and offline access for mobile and web applications.

## Amplify - (set of tools to develop fast full-stack applications, with authentication, hosting, storage, APIs, etc..)

- AWS Amplify is a set of tools and services that helps developers build scalable full-stack applications powered by AWS. It includes features for hosting, authentication, storage, and APIs, streamlining the development process.

## AWS Application Composer - (AWS Infrastructure as code, visually desing and build serverless applications)

- AWS Application Composer is a visual tool that helps you design and build serverless applications by dragging and dropping components. It simplifies the process of creating applications on AWS Lambda and other serverless services.

## Device Farm - (Test your applications in REAL browsers, mobile devices, etc..)

- AWS Device Farm is an application testing service that lets you test your mobile and web applications on a wide range of real devices hosted in the cloud. It provides automated and manual testing capabilities to improve app quality.

## AWS Backup - (centrally manage and automate backups with BACKUP PLANS)

- AWS Backup is a centralized backup service that automates and centrally manages backups across AWS services. It helps ensure compliance and data protection by providing backup solutions for various AWS resources.

## AWS Disaster Recovery Strategies

- **Backup and restore**: cheapest cost, but your data will "return in time" if your app was running.
- **Pilot Light**: medium cost, maintains a minimal version of an application in the cloud for quick restoration during a disaster.
- **Warm Standby && Multi-site/Hot-site**: expensive cost, full version of the application running.

## AWS Elastic Disaster Recovery (DRS) - (block level replication of your servers in the cloud)

- AWS Elastic Disaster Recovery (DRS) provides continuous replication of your on-premises and cloud-based applications to AWS. It allows you to quickly recover applications and data in the event of a disaster with minimal downtime.

## CloudEndure Disaster Recovery - (rapid recoveyr and minimal downtime in case of failures)
- A disaster recovery solution that enables continuous replication of applications and data.

## AWS DataSync - (move large data from on-premise servers to AWS, incremental replication tasks)

- AWS DataSync is a data transfer service that simplifies moving data between on-premises storage and AWS storage services. It automates and accelerates data transfer for large-scale data migration or synchronization tasks.

## Cloud Migration Strategies - The 7Rs

- **Retire**: Turn off things you don't need, reducing costs, reducing surface areas for attacks.
- **Retain**: Do nothing for now (servers that need compliance, don't need to be migrated, etc..).
- **Relocate**: Move apps from EC2 to different VPC account or Region.
- **Rehost (lfit and shift)**: Migrate your on-premise machines to AWS cloud, you possibly can save some costs of maintenance.
- **Replatform (lift and reshape)**: Migrate your database to RDS, no change the core but leverage Cloud optimizations.
- **Repurchase (drop and shop)**: Moving to a SaaS product, expensive in short term but quickly to deploy.
- **Refactor/Re-architect**: rethinking an application to optimize it for the cloud, enhancing scalability and performance while leveraging cloud-native features.

## Application Discovery Service & Application Migration Service

- **AWS Application Discovery Service** helps organizations understand their on-premises environment for **migration planning**.
- **Application Migration Service**: Automates the migration of applications to AWS, reducing manual efforts and risks.
  - It follows the **Rehost "lift and shift"** strategy

## AWS Migration Evaluator - (Quick insights to migrate from on-premise to AWS Cloud)

- AWS Migration Evaluator provides insights into your current workloads, helping you estimate costs, performance, and migration efforts. It offers data-driven recommendations to optimize your cloud migration strategy.

## AWS Migration Hub - (Central location to discover, analyze, track your migration)

- AWS Migration Hub provides a central location to track the progress of application migrations across multiple AWS and partner solutions. It offers visibility into the status of your migration projects.

## AWS Fault Injection Simulator (FIS) - (Stress an application to verify its resilience by intentionally injecting faults and observing how it responds.)

- AWS Fault Injection Simulator is a managed service that helps you improve application resilience by allowing you to carry out controlled chaos engineering experiments. It helps identify weaknesses in your applications before they occur in real-world scenarios.

## AWS Step Functions - (visual way to orchestrate Lambda functions workflow)

- AWS Step Functions is a serverless orchestration service that enables you to coordinate multiple AWS services into serverless workflows. It allows you to build and visualize workflows, ensuring complex processes run reliably.

## AWS Ground Station - (connect to satellites)

## AWS PinPoint - (Marketing Communication Service)
- Support email, SMS, voice...
- Scales to billions of messages per day.
- Possibility to receive replies.
- Easy to integrate with other AWS services.
- **Use cases**: Run marketing campaigns by sending marketing bulk, transactional SMS messages

  ### Difference from AWS PinPoint and SNS or Amazon Simple Email Service (SES)
  - **AWS SNS & Amazon Simple Email Service (SES)**: Manage on the applications message templates and content for simple notifications and emails.
  - **AWS PinPoint**: Provides advanced message management, including templates, targeting, and analytics for personalized user engagement across multiple channels.