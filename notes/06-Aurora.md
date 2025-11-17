# Amazon Aurora Notes

- Proprietary DB
- Supports Postgres and MySQL compatibility, with drivers etc
- AWS cloud optimized, 5x performance over MySQL, 3x performance over Postgres on RDS
- Storage autoscales in increments of 10GB up to 256TB
- Up to 15 replicas
- Failover in Aurora instant. High availability
- 20% more than RDS

- 6 copies of data across 3 AZ
  - 4 copies out of 6 needed for writes
  - 3 copies out of 6 need for reads
  - (believe these are called read quorum and write quorum) - "self-healing"

- 100s of volumes
- One instance is master


Storage
- Replicated
- Self healing
- Auto expanding

Reader Endpoint - has load balancing, for auto scaled read replicas

Automated patching

### Custom Endpoints

Can define subset of Aurora instances as custom endpoint - used for e.g. analytical queries

### Aurora Severless

Automated database instantiation, no capacity planning

### Global Aurora

Cross Region Read Replicas, or recommended choice: Global Database
- 1 primary region
- up to 10 secondary regions
- up to 16 read replicas per secondary region
- typical replication across globe less than 1 second
- one write primary region, but could promote secondary region to be read/write

### Aurora Machine Learning

- Enable ML-based predictions
- Good integrations with AWS ML services - SageMaker, Comprehend

### Babelfish

- Allow Aurora PostgreSQL to understand T-SQL commands for MS SQL Server

### Aurora Backups

Automated, 1 to 35 days retention, cannot be disabled

Manual DB snapshots, triggered by user, retention as long as you want

### Aurora Database Cloning
- Create new cluster
- Faster than snapshot and restore
- Copy-on-write