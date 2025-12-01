# Amazon Elastic Kubernetes Service (EKS) Notes

- Managed Kubernetes clusters
- Alternative to ECS, same goal, different API
- Kubernetes is open-source tech

Two modes
- EC2 worker nodes
- Fargate serverless containers

Use case: company already using Kubernetes elsewhere and want to migrate to AWS

- EKS Pods rather than ECS Tasks
- EKS Nodes

## Node Types

- Managed Node groups: Nodes (EC2 instances) created for you, ASG managed by EKS
- Self-Managed Nodes: Nodes you create yourself
- AWS Fargate: no maintenance, no nodes managed

## Data Volumes

- Need to specify StorageClass manifest
- Supports EBS, EFS (only works with Fargate), and FSx for Lustre or NetApp ONTAP