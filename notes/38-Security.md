# Security Notes

## AWS KMS (Key Management Service)

- Use in most AWS services
- Two types of encryption
  - Symmetric (AES-256), one key to encrypt and decrypt
  - Asymmetric (RSA and ECC key pairs), public key to encrypt and private key to decrypt

Types of keys
- AWS Owned Keys
- AWS Managed Keys
- Customer managed keys (must pay for these)

Regions by default don't share KMS keys - copying snapshots across region can automatically re-encrypt e.g. EBS volume

### Key Policies

- Similar to S3 bucket policies, but must have them

### Multi-Region Keys

- Primary key in one region, synced with replica keys in other regions
- Identical keys used interchangeably
- Not global, each multi-region key managed independently
- Use for global DynamoDB, global Aurora, global client-side encryption

#### Global DynamoDB

- Can client-side encrypt certain sensitive attributes, e.g. social security number. Data in DynamoDB gets replicated to other regions. Client with the right permissions can still decrypt with multi-region key
- Using Amazon DynamoDB Encryption Client

#### Global Aurora

- Same idea but with AWS Encryption SDK client-side
- Lower latency with key in same region, which can be done with multi-region keys

### S3 Replication

Object encrypted with SSE-KMS need to have replication enabled

### IAM Sharing

- Can share KMS key from source account to target account to decrypt AMI

## SSM Parameter Store

- Secure storage for config and secrets in AWS
- Encryption using KMS
- e.g. store app's config files, unencrypted or encrypted, manage security either way
- Standard or Advanced tiers: advanced can be larger and more, and can have policies

### Policies

- Can assign a TTL to expire
- Can assign multiple policies

## AWS Secrets Manager

- Store secrets
- Force rotation of secrets
- Good integrations
- Encrypted with KMS
- Particularly good for RDS
- Replication across regions. Can promote a read replica to standalone secret

## AWS Certificate Manager (ACM)

- TLS Certificate management, provision, deployment
- For HTTPS certificates
- Automatic renewal, 60 days before expiry
- Free for public TLS certs
- List domain names included in cert, can be wildcards
- DNS validation or email validation
- Can generate outside and import, and then get daily expiration events in EventBridge 45 days before expiration
- AWS Config has a managed rule to check for expiring certs

### API Gateway

- ACM must be in same region for edge-optimized or regional API Gateway

## Web Application Firewall (WAF)

- Layer 7 protection (HTTP)
- For ALB, API Gateway, CloudFront, some others
- NOT on NLB, thats layer 4
- Web ACL (Access Control List) Rules
  - IP matching rules
  - HTTP headers, etc
  - Size, geo
  - Rate-limiting
- Web ACL is regional. Can have rule groups to make them reusable
- When creating a web ACL (protection pack), you can specify one or more CloudFront distributions to you want AWS WAF to inspect.

### Fixed IP with WAF and ALB

- Use Global Accelerator to get a fixed IP for the ALB
- WebACL for WAF must be same region as ALB

## AWS Shield

- Protects from DDoS
- AWS Shield Standard - enabled by default, protection from common attacks
- AWS Shield Advanced: expensive option, protection from sophisticated attacks on common services
  - AWS DDoS reponse team 23/7 access support
  - Automatically manages AWS WAF

## AWS Firewall Manager

- Manage rules is all accounts in AWS org
- Security policy
  - WAF
  - Shield Advanced policies
  - Security Groups
  - VPC Network Firewall
  - Route 53 DNS Firewall
- Applied to existing and future resources

So WAF is for granular control. Firewall Manager for organisational control across all accounts. Shield Advanced for advanced organisational DDoS protection.

## Amazon GuardDuty

- Intelligent threat discovery
- Machine Learning
- 30 days trial
- Reads 
  - CloudTrail data
  - VPC FLow Logs
  - DNS Logs
- Integrate with EventBridge to notify of findings
- Protect against CryptoCurrency attacks

## Amazon Inspector

- Automated security assessment
- EC2, analyse unintended access, known vulnerabilities in OS
- Container Image assessment when pushed
- Lambda Function vulnerabilities in code and dependencies
- Reports to AWS Security Hub
- Send findings to EventBridge
- Only for EC2, ECR, Lambda
- Risk score for prioritization

## Amazon Macie

- Use machine learning and pattern matching to protect sensistive daata
- Help identity PII (Personally Identifiable Information)
- Use only for S3 bucket data