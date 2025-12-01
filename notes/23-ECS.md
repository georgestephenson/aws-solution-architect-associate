# ECS - Elastic Container Service Notes

- Launch a Docker container in AWS - ECS Task on ECS Cluster

## EC2 Launch Type 

- Cluster comprises EC2 instances, running the ECS Agent for the cluster
- Once set up, AWS handles starting and stopping many containers in the EC2 instances in the cluster

## Fargate Launch Type

- Serverless (no EC2 management)
- Task definitions, ECS tasks run based on CPU/RAM requirements.
- Scaling just involves increasing number of tasks

## IAM Roles

- EC2 Instance profile used by ECS agent (for EC2 launch type). Makes API calls, sends logs, pulls Docker image, gets secrets
- ECS Task Role - each task has a specific role. Valid for both launch types (EC2 and Fargate). Can link to different AWS services with different roles.

## Load Balancing

- ALB recommended for most use cases, NLB only recommended for high throughput, or to pair with AWS Private Link

## Data Volumes with EFS

- Can mount EFS on ECS tasks
- Fargate with EFS will be completely serverless - for multi-AZ shared storage

## Auto Scaling

- Can increase/decrease ECS tasks with ECS Auto Scaling, which uses AWS Application Auto Scaling

Can scale on metrics:
- CPU Utilization
- RAM (Memory Utilization)
- ALB Request Count Per Target

Scale on target metric, steps based on alarm, or scheduled

Task scaling not same as EC2 auto scaling. Fargate much easier as it is serverless.

### EC2 Instance scaling

Option 1: Auto Scaling Group
Option 2: ECS Cluster Capacity Provider, auto scale infrastructure for ECS tasks. Pairs with ASG. Smarter

### Solutions Architectures

Lots of examples of EventBridge sending events to and from ECS Tasks or Clusters to other AWS services, for a serverless architecture

## Amazon ECR (Elastic Container Registry)

- Store and manage Docker images
- Public and Private repository
- Fully integrated with ECS
- Access control through IAM between ECR/ECS