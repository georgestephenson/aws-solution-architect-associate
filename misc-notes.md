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