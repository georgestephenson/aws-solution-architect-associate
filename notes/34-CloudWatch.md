# Amazon CloudWatch Notes

## CloudWatch Metrics

- Provides metrics for every AWS service
- Dimension = attribute of a metric, metadata, up to 30 of them
- CloudWatch dashboards of metrics
- Custom metrics

### Metric Streams

- Stream metrics for near real time delivery
  - Kinesis Data Firehose
  - 3rd party services like Datadog, Splunk, etc.

## CloudWatch Logs

- Log groups: typically application
- Log stream: instance within application, specific log files, specific containers
- Expiration policy
- Export, stream to other AWS services like S3, Kinesis Data Streams, etc.
- Lots of sources for logs
- S3 Export batch job
- Use Logs Subscriptions for real-time logging events
  - Can stream logs to Amazon OpenSearch with CloudWatch logs subscription
- Can do log aggregation with subscription filters
- Can send logs to other accounts with cross-account subscription, configuring IAM role and access policy to deliver to kinesis data streams

### Logs Insights

- Apply query to logs, gets results and visualization

### Logs on EC2

- By default, no logs from EC2 to CloudWatch
- Need to run CloudWatch agent on EC2 to push to CloudWatch
- EC2 instance needs IAM role for this

## CloudWatch Agents

- Log Agent: old agent
- Unified Agent: collect additional metrics, and can send logs
- Unified Agent collects much more metrics than just disk and CPU for EC2 or Linux server

## CloudWatch Alarms

Alarm states:
- OK
- INSUFFICIENT_DATA
- ALARM

### Targets

- Act on an EC2 instance: stop, reboot, etc.
- EC2 Auto Scaling, alarm will trigger scaling
- notification to SNS, then onwards to pretty much anywhere

### Composite Alarms

- Multiple alarm combined, AND or OR conditions

## CloudWatch Container Insights

- Metrics and logs from containers
- ECS, EKS, Kubernetes on EC2, Fargate (ECS/EKS)
- Needs containerised version of CloudWatch Agent in EKS/Kubernetes

## CloudWatch Lambda Insights

- Lambda metrics
- Dashboard specific to Lambda functions

## CloudWatch Contributor Insights

- Find "top talkers", who or what has most impact on services
- e.g. Identify heaviest network users

## CloudWatch Application Insights

- Metrics for monitored application on EC2 instances for select technologies (Java, .NET, etc)