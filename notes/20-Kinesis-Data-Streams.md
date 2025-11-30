# Amazon Kinesis Data Streams Notes

- Real-time streaming data collection and storage
- For real-time data sources, like IoT devices, metrics and logs
- Produced by apps or Kinesis Agents on your servers
- Consumers can be apps, Lambda functions, Data Firehose, managed service for Apache Flink
- Retention up to 265 days
- Ability to replay/reprocess by consumers
- Can't delete data until expired
- Data up to 1MB
- Ordering guarantee within same Partition ID
- Encrypted HTTPS in-flight and KMS at-rest
- Kinesis Producer Library and Kinesis Client Library to write code to use

## Capacity Modes
- Provisioned mode: choose number of shards: each shard is 1MB/s in 2MB/s out
  - Adjust number of shards to how much throughput you need

- On-demand mode: scales automatically based on last 30 days, default provision is 4MB/s