# Auto Scaling Group (ASG) Notes

- Scale out (add EC2 instances)
- Scale in (remove EC2 instances)
- Min and max EC2 instances
- Auto register new EC2 instances to load balancer
- Re-create EC2 instance if previously terminated

ASG is free, only pay for resources e.g. EC2 instances

Set in Auto Scaling Group
- min capacity
- desired capacity
- max capacity

ELB can work with ASG to scale out and in, terminate unhealthy instances

#### Group Attributes
- Launch Template: AMI, EB2 User Data, Secuirty Groups, SSH Key Paid, IAM Roles, etc
  - Very similar to launching an EC2 instance as it launches many EC2 instances
- Min/Max/Initial Capacity
- Scaling Policies

CloudWatch Alarms 
- Can trigger scaling
- Alarms based on metrics, e.g. average CPU

### Scaling Policies
- Dynamic Scaling
  - Target Tracking Scaling, e.g. want to keep average CPU at 40%
  - Simple / Step Scaling, e.g. if above target, add 1
- Scheduled Scaling
  - Scale at specified times of days, or other schedules
- Predictive Scaling
  - Forecase load and scale capacity ahead of time

#### Good Scaling Metrics
- CPUUtilization
- RequestCountPerTarget, number of requests to EC2 instances
- Average Network In / Out
- Custom using CloudWatch

After scaling, you are in cooldown period, the ASG won't launch or terminate more during cooldown period.

## Launch Configuration vs Launch Template

Launch template newer and now what AWS recommends. Recommend to migrate to Launch Template

### Launch Configuration

- Document with information for provisioning an EC2 instance, same as you would do manually
- Can't be modified after creation
- Only for ASGs
- Can't create new ones now. So basically deprecated.

### Launch Template

- Similar but more versatile
- Can use for a one-off EC2 instance, spot fleet, or ASG
- Versioned, so can be changed