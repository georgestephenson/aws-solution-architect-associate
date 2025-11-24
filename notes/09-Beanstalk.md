# Elastic Beanstalk Notes

- Uses all the same components like EC2, ASG, ELB, RDS, but as a managed service for developers to run their app
- Automatic scaling, load balancing, monitoring, etc.
- Only worry about the app code
- Beanstalk is free, but pay for the instances e.g. the EC2 instances it creates
- Support loads of languages, plus docker single and multi containers

## Web Server Environment Tier vs Worker Environment Tier

- Web server has an ELB and web environment for users
- Worker environment has an SQS queue for worker to process jobs

## Deployment modes

- Single instance might be useful for dev
- High Availability with Load Balancer good for prod