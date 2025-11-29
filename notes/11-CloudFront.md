# CloudFront Notes

- CDN
- Hundreds of Points of Presence around the world (edge locations and caches)
- DDoS protection, integration Shield and AWS Web App Firewall

## Origins

- S3 Buckets, using Origin Access Control (OAC)
- VPC Origin: VPC, privately connect to ALB, NLB, EC2
- Any custom HTTP origin, S3 website or outside AWS

## vs Cross Region Replication

- Replication is not caching, files updated in near-real time
- Cross-region replication must be setup in specific regions, but good for replicating dynamic contant fast
- CloudFront great for caching all around the world.

## Using ALB/EC2 as Origin

- Best way: VPC Origins
- Can expose your private subnet to CloudFront which provides access to public
- Used to have to have a public network EC2 to use CloudFront

## Geo Restriction

- Allowlist or Blocklist of countries where users allowed to access content

## Pricing

- Depends on edge location geographic region
- Reducing edge locations reduces cost
1. Price Class All - all regions, best performance
2. Price Class 200 - most regions, excludes expensive regions
3. Price Class 100 - least expensive, least regions

## Cache Invalidation

- CloudFront Invalidation : bypass TTL to refresh cache. Invalidate all files (\*) or special path (/images/\*)