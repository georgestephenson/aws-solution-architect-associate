# AWS Lambda Notes

- Virtual functions
- No servers to manage
- Short executions
- Run on-demand
- Automated scaling
- Pay per request and compute time
- Generous free tier
- Loads of integrations with programming languages, AWS services
- Can run container images, but must implement Lambda Runtime API (ECS usually preferred though)

## Lambda Limits Per Region

### Execution
- Memory Allocation: 128MB - 10GB (1MB increments)
- Max exec time: 900 seconds
- Env vars: 4kb
- Disk capacity: 512MB - 10GB
- Concurrent executions 1000

### Deployment
- Function size compressed 50MB
- Function size uncompressed 250MB
- Can use /tmp to load other files
- Env vars: 4kb

## Concurrency

- Reserved concurrency: limit on number of concurrent functions
- If sync invocation: return ThrottleError 429
- If async invocation: return automatically
- Account has a limit so don't want one function throttling other functions

## Cold Start

- New instance when code is first run, if init is large, might be slow

## Provisioned Concurrency

- Avoids delay caused by cold start by pre-allocating concurrency
- "Reserved" just means the function is guaranteed to be able to scale to a max number of instances. "Provisioned" will actually pre-start the instances.

## Lambda SnapStart

- Improves performance up to 10x for Java, Python and .NET
- Will invoke function pre-initialised (no init phase)
- Takes snapshot of function after init

## Edge Function

- Run functions closer to users (at the edge)

Two types: CloudFront Functions, Lambda@Edge

### CloudFront Functions

- JavaScript, for CDN customisation
- Used to change the Viewers requests and responses
- Native to CloudFront
- Very high scale, millions of requests per second
- Very short funcion < 1ms

### Lambda@Edge

- NodeJS or Python
- Used to change CloudFront request and responses, Viewer or Origin
- Thousands of requests per second

### Lambda in VPC

- By default Lambda outside your VPC in AWS's own VPC
- Can specify your VPC, subnet and security groups
- Lambda creates ENI in your subnet
- Lambda with RDS DB proxy: direct Lambda connection would open too many connections. RDS proxy will pool DB connections.
- RDS proxy never public, so Lambda needs to be in your VPC.

### RDS and Aurora

- Can process data events with Lambda functions
- RDS can invoke the Lambda, to e.g. send email
- Must allow outbound traffic from DB, and have required permission with IAM policy to invoke function
- RDS event notifications are different data events. They are events about the DB itself not the data. They can be pushed to SNS or EventBridge then onto Lambda.

## Step Functions

- Orchestrate Lambda functions with visual workflow
- Can orchestrate other AWS services too
- Can add human approvals

## Layers

- ZIP archive of libraries or other dependencies. Layers can be used in Lambda function without needing to be in deployment package.