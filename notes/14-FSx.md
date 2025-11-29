# Amazon FSx Notes

- For 3rd party high-performance file systems
  - Lustre
  - Windows File Server
  - NetApp ONTAP
  - OpenZFS

## Windows File Server

- Fully managed share drive
- SMB protocol and Windows NTFS
- Active Directory integration,
- Can be mounted on EC2 instances
- Can group together using Distributed File System (DFS)
- Scales very large and fast
- Storage options SSD, HDD
- Access from on-premises
- Can be multi-AZ
- Backed up daily to S3

## Lustre

- Distributed for large scale computing
- Lustre = Linux + Cluster
- Use case: machine learning, high performance computing
- Scales very large and fast
- Storage options SSD, HDD
- Seamless integration with S3
- Can write output to S3
- Use from on-premises (VPN or Direct Connect)

### Deployment options
- Scratch File System, temporary short-term processing, data not replicated, very fast
- Persistent File System, long-term, replicated within AZ, for long-term processing

## NetApp ONTAP

- Managed service
- NFS, SMB, iSCSI protocol
- Migrate workloads running on ONTAP or NAS to AWS
- Broad compatibility with AWS and on-premises
- Instantaneous cloning

## OpenZFS

- Managed service
- Compatible with NFS
- Use case to migrate ZFS systems to AWS
- Broad compatibility
- Up to 1 million IOPS
- Instantaneous cloning
