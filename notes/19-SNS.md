# Amazon SNS Notes

Simple Notification Service (SNS)

- One message to many receivers
- Using a SNS topic, Pub/Sub model decouples service from recipients
- Each subscriber gets all messages
- Up to 12.5M subscriptions per topic
- Up to 100k topics
- Send emails, SMS, HTTPS endpoints, SQS, Lambda, Kinesis Data Firehose
- Many AWS service can send to SNS

Use Topic Publish SDK to publish to a topic

Direct Publish (mobile apps SDK) - create and publish to a platform endpoint (Google, Apple, Amazon) for mobile app push notifications

## Security

- In-flight encryption with HTTPS
- At-rest encryption, KNS keys
- Client-side encryption possible
- Access controls: IAM policies
- SNS Access Policies

## SNS + SQS Fan Out Pattern

- Push to an SNS topic once, many SQS queues are subscribers
- SQS allows delayed processing and retries
- Can add more SQS queues for more use cases
- Cross-Region Delivery
- Use case: 
  - S3 event to multiple queues. S3 events limited to one rule. Can send event to SNS then fan-out.
  - Kinesis Data Firehouse can send from SNS to any S3 or other data destinations
- Can also fan-out SNS FIFO to SQS FIFO.
- Message filtering: JSON policy to filter messages sent to each SNS subscriber. So the subscription has the JSON policy.

## SNS FIFO

- Like SQS FIFO
- Ordering
- Deduplication with ID or content-based
- Limited throughput
- Only SQS can subscribe to SNS FIFO, though it can be standard or FIFO SQS