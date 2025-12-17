# Amazon DynamoDB Notes

- Key-value and document database (commonly called NoSQL)
- Fully managed, highly available, multi-AZ replication DB
- NoSQL with transactions
- Millions of requests per sec, trillions of rows, 100s of TB
- IAM security
- Low cost
- No maintenance

## Basics

- Tables have primary keys
- Items = rows
- Items have attributes
- Max item size 400kb, not for large data
- If schema needs to rapidly evolve - pick DynamoDB (NOSQL)

## Modes

- Provisioned Mode: specify reads/writes per second, pay for provisioned read and write units. The key thing about provisioned mode is that it reduces cost. You can enable auto-scale in provisioned mode.
- On-Demand Mode: auto-scale, pay for anything you use, more expensive but better if unpredictable load

## DynamoDB Accelerator (DAX)
- In-memory cache
- Solves read congestion on DB with caching
- No app logic changes required, works with same APIs
- Default 5 minutes TTL on cache
- Compared to ElasticCache, DAX caches DynamoDB objects and queries, whereas ElastiCache could be used for aggregation results.

## Stream Processing

- Ordered stream of item modifications in table
- Could be for real time analytics
- Send to DynamoDB Streams, or Kinesis Data Streams for higher max consumers and more services support

## Global tables

- Two-way replication between tables in regions
- Must have DynamoDB stream enabled to use as this powers the two-way replication

## TTL

- Auto delete items after expiration timestamp
- Use cases: reduce stored data, regulatory obligations, session data

## Backups

- Continuous backups with point-in-time recovery. Optional for last 35 days
- On-demand backups for long-term retention, configure and manage with AWS Backup

## S3

- Can import from and export to S3