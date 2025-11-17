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
- To encrypt use backup and restore
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