# Miscellaneous Notes

## Instantiating applications (fast)

### EC2

- Golden AMI: install applications into an image, launch EC2 instances quickly from AMI
- Dynamic config with User Data scripts, so hybrid of Golden EMI and User Data

### RDS

- Restore from snapshot, schemas and data ready

### EBS 

- Restore from snapshot, formatted, data ready

## SQS vs SNS vs Kinesis

- SQS consumers pull data, SNS pushes data to subscribers, kinesis standard is pull data (2MB/s per shard) or enhanced fan-out is push (2MB/s per shard per consumer)
- SQS data deleted after being consumed, SNS data not persisted if not consumed, Kinesis can replay data until it expires after X days
- Kinesis for real-time big data

## App2Container

Automated tool to convert Java and .NET web apps to Docker images that can be run in AWS

Automatically create CloudFormation template to create ECS Task or EKS Pod definitions

Docker image goes to ECR

Deploy to ECS/EKS/AppRunner

## Other Databases

### DocumentDB

- AWS-implementation layer for MongoDB NoSQL database
- Fully managed, highly available, replication across 3 AZ

### Nepture

- Fully managed graph database
- Highly available, replication across 3 AZ
- Use cases: wikipedia database is knowledge graph, social networking
- Steams: real-time ordered sequence of changes to graph DB. REST API for this. No duplicates, strict ordering.

### Amazon Keyspaces

- Managed Apache Cassandra database, serverless, auto-scaling, replicated across AZ.

### Amazon Timestream

- Time series database. Data plotted against time.
- Much faster and cheaper for time series data than relational databases.