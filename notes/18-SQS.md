# Amazon SQS Notes

Simple Queue Service (SQS)

- Can have many producers of messages, feeding into an SQS Queue
- Many consumers can poll messages from the queue
- Decouples producers from consumers
- Oldest offering, fully managed service

## Attributes

- Unlimited throughput and num of messages in queue
- Default retention of messages 4 days, max 14 days
- Low latency
- Limitation of 1,024kb per message
- Can have duplicate message (at least once delivery)
- Can have out of order messages (best effort ordering)

### Producers

- Send using SDK (SendMessage API)
- Persisted in queue until deleted by consumer

### Consumers

- Could be running on EC2 instances, Lambda functions, on-premises...
- Polls SQS for messages, get up to 10 at a time
- Processes the messages, e.g. insert into RDS database
- Delete message using DeleteMessage API
- Can have multiple consumers - parallel EC2 instance computing
- At least once delivery, could be processed by multiple consumers
- Can scale horizontally to process more messages

### Auto Scaling Group (ASG)

- Can scale consumers with ASG
- Can use Queue Length as a metric with which to scale consumers
- Then set CloudWatch Alarm when queue over X length (we are lagging behind, queue is getting big)
- For spikes of activity on DBs, use SQS as a buffer between auto-scaling apps, and the DBs
- Then have another auto-scaling group to dequeue messages.
- SQS queue is infinitely scalable so deals with decoupling between auto-scaling groups, e.g. frontend ASG and backend ASG

### Security

- In-flight encryption with HTTPS
- At-rest encryption with KMS keys
- Can have client-side encryption (obviously)
- IAM policies can be used to restrict access
- SQS Access Policies, like S3 bucket policies, useful for cross-account access, and allowing other AWS services access

## Message Visibility Timeout

- When message polled by consumer, becomes invisble to other consumers
- By default, timeout is 30 seconds during which it will be invisible to others
- After timeout, same message is visible again. So could be processed twice if not processed and deleted during timeout window
- Can call ChangeMessageVisibility API to change timeout window
- If timeout is high, if consumers crashes, it won't get re-processed for long time. If too low, duplicate processing likely to happen

## Long Polling

- Consumer can wait for messages to arrive it there are none in the queue
- Long polling because API call for polling is long and infrequent

## FIFO (First In First Out) Queue

- Producer sends message in specific order - consumer reads in same order
- Limits throughput
- Exactly once send capability (using deduplication ID)
- Ordering by group ID, messages for a group will be ordered within the group