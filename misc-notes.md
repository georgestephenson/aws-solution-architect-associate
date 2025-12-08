# Miscellaneous Notes

## Instantiating applications (fast)

### EC2

- Golden AMI: install applications into an image, launch EC2 instances quickly from AMI
- Dynamic config with User Data scripts, so hybrid of Golden EMI and User Data. Point here is using User Data for dynamic config, but not for the actual installation itself.

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

### Neptune

- Fully managed graph database
- Highly available, replication across 3 AZ
- Use cases: wikipedia database is knowledge graph, social networking
- Steams: real-time ordered sequence of changes to graph DB. REST API for this. No duplicates, strict ordering.

### Amazon Keyspaces

- Managed Apache Cassandra database, serverless, auto-scaling, replicated across AZ.

### Amazon Timestream

- Time series database. Data plotted against time.
- Much faster and cheaper for time series data than relational databases.

## Data and Analytics

### Amazon EMR

- Elastic MapReduce
- Big clusters of hundreds of EC2 instances for creating Hadoop clusters for big data applications
- Fully managed service for Apache Spark, Flink, etc

### Amazon QuickSight

- BI service for interactive dashboards, like Power BI
- SPICE engine, in-memory computation when data imported into QuickSight
- Column-Level Security (CLS)
- Integrates with lots of AWS data sources, most of them
- Common to see with Athena or Refshift
- QuickSight has users and groups, different to IAM users

### AWS Glue

- ETL service
- Prepare for analytics in e.g. Redshift Data Warehouse
- Use case: e.g. convert CSV from S3 to Parquet back to S3, for Redshift analysis, columnar data more performant for analysis
- Glue Data Catalog uses Glue Data Crawler to discover data sources across AWS services and track metadata. Central to many analytics service like Athena, Redshift Spectrum, and EMR.

### AWS Lakes Formation

- Data lake - fully managed service to setup your data lake
- Combine structured and unstructured data
- Simplifies security when you many data sources and users accessing them all from e.g. Athena and Quicksight 

### Managed Service for Apache Flink

- Apache Flink - framework for processing data streams

### Managed Service for Apache Kafka (MSK)

- Alternative to Amazon Kinesis
- Fully managed Apache Kafka
- Deploy MSK to your VPC, multi-AZ, or Serverless option without managing capacity.
- Kinesis Data Streams with Shards = Kafka Topics with partitions

## CloudFormation

- Declarative way of outlining AWS Infrastructure
- Infrastructure as Code
- Declarative code
- Sounds similar to Terraform
- Can visualise using Infrastructure Composer

### CloudFormation Service Role

- IAM roles
- Even if user doesn't have permission on resources directly
- User must have iam:PassRole permission

## Simple Email Service (SES)

- Managed service to send emails
- Reputation, performance, anti-spam

## Amazon Pinpoint

- 2-way marketing communications
- SMS, email, push, voice, in-app messaging
- SNS and SES allow fine-grain notifications and emails whereas Pinpoin is full marketing campaign management

## Systems Manager

### SSM Session Manager

- Secure shell to your EC2 through service with IAM permissions, no port 22 needed in EC2 instance

### Run Command

- Run command across multiple instances without SSH

### Patch Manager

- Automate patching managed instances
- EC2 instances, on-premises servers
- On-demand or scheduled

### Maintenance Windows

- Schedule actions on servers, could be OS patching, drivers, installing software

### Automation

- Common maintenance or deployment task on EC2 or other AWS resources
- e.g. restart instances

## Cost Explorer

- Manage AWS costs
- Custom reports
- Choose optimal Savings Plan. Savings Plan feature is an alternative to Reserved Instances.
- Forecasts of usage and cost

## AWS Cost Anomaly Detection

- Use ML to detect unusual cost patterns, spikes, increases, etc.
- Monitors service
- Root-cause analysis
- Anomaly detection report
- Daily/weekly summary sent using SNS

## AWS Outposts

- AWS provided service racks for hybrid cloud implementations
- Can use AWS services on-prem as if you're in the cloud
- Called "Outposts Racks"
- Difference is you're responsible for security of the rack

## AWS Batch

- Fully managed batch processing
- Batch jobs, can run 100,000s of them
- Dynamically launch EC2 instances or Spot Instances
- Docker images and run on ECS
- Unlike Lambda, no time limit in Batch

## Amazon AppFlow

- Securely transfer data between SaaS apps and AWS
- From e.g. SAP, Salesforce, ServiceNow, Slack, Zendesk
- Schedule, event-driven or on-demand

## AWS Amplify

- Web and mobile dev tool
- Amplify CLI can configure all the AWS resources need for your app
- Amplify Frontend Libraries like React, Flutter, etc
- Deploy using Amplify Console

## Instance Scheduler

- Through CloudFormation, schedule instances to start/stop automatically
- Schedules managed in DynamoDB
- Cross-account and cross-region