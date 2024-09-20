# AWS Cloud Integrations

## Synchronous Communication

- When a service directly communicates with another and expects an immediate response.
- E.g.: buying service -> shipping service
- Can be problematic if there are sudden spikes of traffic.
- In this case is better to decouple it into asynchronous services.
  - Using SQS, SNS, Kinesis for real-time data streaming.

## Asynchronous/Event Based Communication

- When services communicate without expecting an immediate response. The requesting service sends a message or event that is after processed.
- E.g.: buying service -> queue -> shipping service

## Amazon SQS - Simple Queue Service

- Producer: Send messages to the SQS queue
- Consumer: Pull data from the SQS queue.
- **Pull-based**: Messages are stored in the queue and consumers need to fetch.
- Messages are deleted after they're read by consumers.
- Low latency (< 10ms on publish and receive)
- Consumers share the work to read messages and scale horitzontally.

  ### - Decouple between layers of application.
    - `If you have EC2 instances that receive requests for processing videos.`
    - Use separate EC2 instances with an Auto Scaling Group to handle incoming video requests and save them to an AWS SQS Queue.
    - Another set of EC2 instances, with a different Auto Scaling Group, pulls messages from the queue to process the videos.

  ### - AWS SQS - FIFO Queue
    - First in first out. (Ordering of the messagens in the queue.)
    - Messages are consumed in order by the consumer.

## Amazon SNS - Simple Notification Service
- The **event publishers** only send message to one SNS Topic.
- As many **event subscribers** as you want to listen to SNS topic notifications.
- Each subscriber to the topic will get all the messages.
- With SNS you can send the events to many services like, SQS, Lambda, and also Send Emails, SMS, and HTTP requests.
- **Push based**: Messages are automatically delivered to the subscribers.

## Amazon Kinesis - Real-time Big data Streaming
- Managed service used to collect, process, and analyze real-time sharing data at any scale.

## Amazon MQ
- SQS, SNS are "cloud-native" services: proprietary protocols from AWS.
- Traditional services running from on-premises may use open protocols: MQTT, AQMP, STOMP, OpenWire, WSS.
- When migrating to the cloud instead of re-engineering all the application to use SQS and SNS, we can use Amazon MQ.
- Amazon MQ is a managed broker service for RabbitMQ and ActiveMQ.
