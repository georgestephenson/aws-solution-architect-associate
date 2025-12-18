# Relational Database Service (RDS) Notes

- Managed DB service for SQL language DBs

## Supported DBs

- Postgres
- MySQL
- MariaDB
- Oracle
- MS SQL Server
- IBM DB2
- Aurora AWS

Managed service, as opposed to running a DB on EC2
- Automated provisioning, OS patching
- Continuous backups, restore to timestamp
- Monitoring dashboard
- Disaster recovery, multi AZ

Downside - can't SSH into instances

## RDS - Storage Auto Scaling

- Storage scales automatically when you're running out of free space
- Set Maximum Storage Threshold
- Support all RDS database engines

## RDS Read Replicas vs Multi AZ

- Read replicas scale read with read-only DBs
  - Can be: within AZ, cross AZ, cross region
  - ASYNC replication
- Use case of Read replicas: reporting DB.
- Network cost if replication goes across AZs.

### RDS Multi AZ (Disaster Recovery)

- SYNC replication (instead of ASYNC)
- One DNS name, automatic failover
- Increase availability
- Not used for scaling

Read replicas *can* be set as Multi AZ for Disaster Recovery as well, so one of the read replicas would be promoted during the failover - but they are distinct concepts.

## RDS - Single AZ to Multi AZ

- Zero downtime needed
- Just click modify on DB
- What happens:
  - Snapshot taken
  - New DB restored from snapshot
  - DBs synchronised

## RDS Custom
- For Oracle and SQL Server
- RDS still automates, but have access to underlying database and OS
  - Configure settings
  - Install patches
  - Access the underlying EC2 instance using SSH
- Recommended to deactivate Automation Mode

## RDS Backups
- Automated daily back ups
- Transaction logs backed up every 5 minutes
- 1 to 35 days of retention, set to 0 to disable

Manual DB snapshots
- Manual, retain as long as you want

Trick - snapshot DB instead of leaving it stopped, to save money

Can restore MySQL RDS from S3
- Create a backup of on-premises
- Store it in Amazon S3
- Then restore into RDS

For Aurora, can do a similar backup using Percona XtraBackup

## Security - RDS or Aurora

- At-rest encryption using AWS KMS
- To encrypt use backup and restore. You can encrypt a snapshot of a DB instance, then restore it. You can't encrypt a DB instance directly.
- In-flight encryption, TLS, use AWS TLS root certificate
- IAM Auth
- Security Groups, control network access
- No SSH, except RDS Custom
- Audit logs, sent to CloudWatch Logs

## RDS Proxy

- Fully managed proxy
- Allows app to share DB connections
- Improves DB efficiency
- Reduce failover time
- Must be accessed from VPC not publicly
- Lambda functions - can scale to many functions, for RDS proxy can pool all into RDS proxy (which is itself scalable)
- Allows you to use IAM roles instead of database connection string to connect.

## SSL

RDS can be configured to SSL certificates in transit.

## Option Groups

- Specify features to apply to one or more instances
- Could be SQL Server/Oracle "transparent data encryption (TDE)"
- Or MySQL/MariaDB audit plug-in to log logons and queries
- Or Oracle S3 integration
- Requires more memory to enable

## Instance Classes

- Standard - db.m6i
- Memory Optimized - db.x1e, 3904GB of memory
- Burstable Performance - for dev/test. db.t4g.

## IOPS

- IOPS will measure how many pages of data can be written to. 
- MySQL/MariaDB pages are 16kb, Oracle/PostgreSQL/MSSQL is 8kb.
- So generally, smaller pages means more IOPS required to read 100MB.
- However, AWS would count a 64kb page as 2 IOPS, max in 1 IOPS is 32KB, so not quite this simple.

## Storage types

### General-Purpose SSD (gp2)

- Up to 16000 IOPS, proportional to disk size.
- Bursting: small volumes get some temporary bursts to 3000 IOPS for spikes in demand, according to a formula. This uses your "credit balance" for IOPS. Replenishes over time to the max of 5.4M credits.

### Provisioned IOPS SSD (io1)

- Specify IOPS number you need.
- Up to 256,000 IOPS.

### Magnetic Storage (Standard)

- Being phased out, max 1TB and 100 IOPS.