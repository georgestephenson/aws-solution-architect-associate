# Disaster Recovery Notes

Preparing for disaster

- On-premises to on-premises
- On-premises to cloud
- Cloud Region A to Cloud Region B

## RPO and RTO

### Recovery Point Objective (RPO)

- How often you run backups
- How much data loss can you accept if a disaster happers

### Recovery Time Objective (RTO)

- How fast you can get online again after a disaster

## Disaster Recovery Strategies

Strategies from high RPO to low RPO

### Backup and Restore (High RPO)

- Inexpensive but high RPO
- Scheduled backups and snapshots

### Pilot Light

- Small version of app in cloud is always running
- Data replication into cloud for pilot light database
- For critical core systems

### Warm Standby

- Full system running as backup, but minimum size
- Scale to production size after disaster

### Multi Site / Hot Site (Very Low RTO)

Full production site running in AWS, full redundancy

### All AWS Multi Region

- Multiple AWS regions, Aurora Global database for full replication

## Database Migration Service (DMS)

- Migrate databases to AWS
- Same platform or to different platform
- Uses an EC2 instance to run
- Source can be on-prem or EC2 instance database, Azure, RDS, S3, DocumentDB
- Targets can be on-prem or pretty much any AWS DBs

Database Migration Service (DMS) is a very fast way to migrate between different database setups with minimal setup, e.g. between S3 buckets and Kinesis Data Streams, or between RDS Databases and Amazon Redshift data warehouse

### AWS Schema Conversion Tool (SCT)

- Convert schema from one DB engine to another
- Don't need SCT if you're going Postgres to Postgres, but need it for Oracle to Postgres etc

### Multi-AZ

- When enabled, DMS has a synchronised replica

## RDS to Aurora MySQL

Option 1: Take DB snapshot and restore. May need some downtime
Option 2: Create Aurora read replica from RDS MySQL, then promote to its own cluster, may take time and money

If external MySQL to aurora MySQL, 
- Option 1: use Percona XtraBackup to create backup in S3 and create Aurora from S3 backup
- Option 2: use mysqldump utility to migrate

Last option: use DMS

## On-Premise strategy

- Can download Amazon Linux 2 AMI as VM
- VM Import / Export
- AWS Application Discovery Service, can scan on-premises servers to plan a migration. Track with AWS Migration Hub.
- AWS Database Migration Service (DMS), replicate until ready to promote cloud replica to the primary database
- AWS Application Migration Service (MGN), incremental replication of on-premises servers

## AWS Backup

- Centrally manage and automate backups for AWS services
- No custom scripts or manual processes
- Cross-region backups for disaster recovery
- Cross-account backups
- PITR, on-demand and scheduled backups
- Backup Plans are policies for frequency and windows and storage types and retention periods

## AWS Backup Vault Lock

- WORM (Write Once Read Many) for all backups
- Even root user can't delete backups

## VMware Cloud on AWS

- Customers might have on-premises Data Center on VMware Cloud
- Can continue to use VMware Cloud software in AWS