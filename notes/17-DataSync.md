# AWS DataSync Notes

- Move large amounts of data (synchronise data hence the name)
- Move on-premises or other cloud to AWS storage, needs agent
- Or AWS to AWS, no agent needed
- Sync to S3, EFS, or FSx
- Replication on schedule
- File permissions and metadata are preserved

EXAM NOTE: unique AWS option for file transfer that will preserve all of the file metadata

- Agent can take up a lot of bandwidth
- You install DataSync Agent on-premises, it talks to AWS via TLS

EXAM NOTE: if we don't have network capacity for DataSync, think about Snowball device