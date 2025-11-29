# AWS Snowball Notes

- Physical, very rugged device to securely transfer data into and out of AWS
- Up to Petabytes of data
- Two types
  - Snowball Edge Storage Optimized (210TB)
  - Snowball Edge Compute Optimized (28 TB)
- Main use case: Much faster than internet transfer for large data volumes e.g. 1 PB. Time to transfer 1 PB at 100 Mbps is 3 years.
- Other use case: edge locations, a ship, a mining station underground. No internet access, or limited
  - Setup Snowball Edge to run EC2 instances, Lambda functions, etc

## Snowball to Glacier

- Can't import direct to Glacier: use S3 first, with lifecycle policy to Glacier