# AWS Storage Gateway Notes

Cloud native storage options
- Block: EBS, EC2 instance store
- File: EFS, FSx
- Object: S3, Glacier

Storage Gateway bridges between on-premises data and cloud data
- Hybrid Cloud
- Use cases: disaster recovery, backup, on-premises cache for data in AWS
- Storage Gateway and EFS can provide low latency access for many EC2 instances

## S3 File Gateway

- Connect S3 bucket to on-premises network with an S3 File Gateway
- Take NFS/SMB on local network, translated to HTTPS to AWS S3 by gateway
- Most recent files cached in gateway
- Bucket access using IAM roles

## Volume Gateway
- Block storage, iSCSI protocol
- Backed by EBS snapshots
- Cached Volumes for low latency access, or Stored Volumes with entire data on-premises, scheduled backups to S3

## Tape Gateway

- For companies with physical tape back ups.
- Same process but in AWS 
- Virtual Tape Library (VTL)
- Virtual tapes in S3, to then be archived in Glacier with lifecycle