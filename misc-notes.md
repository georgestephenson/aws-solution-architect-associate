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