# Solution Architecture Case Studies

## WhatIsTheTime.com
- Simply site to tell users the current time
- No database needed
- Should be highly scalable

### Starting simple

- EC2 instance on T2
- Elastic IP address

### Scaling vertically

- Larger instance, M5
- Some downtime while upgrading to M5

### Scaling horizontally

- More instance of M5
- Rather than give users all IPs, use Route 53 to tell users IPs, no elastic IPs

### Adding/removing instances

- TTL means users won't know instance is down
- Make EC2 instances private
- Use Elastic Load Balancer, which is public
- Can't use A record with ELB, must use Alias
- Restricted security groups

### Auto-scaling group

- Rather than set number of EC2 instances, add auto-scaling group for EC2 instances
- Could make ELB Multi AZ to have EC2 instances in multiple AZ

## MyClothes.com
- Shopping cart
- Hundreds of users
- Scalability, try to keep app stateless as possible

### Starting from previous multi AZ example
- Then user can be moved between instances
- User will lose their shopping cart session
- Can enable ELB stickiness - still bad if instance goes down

### Web Cookies
- User stores shopping cart as web cookies
- Stateless but HTTP requests are heavier
- Security risk on cookies
- Cookies must be less than 4KB

### Server Session
- session_id in web cookies
- Store full session in ElastiCache, or alternatively DynamoDB

### Database
- User data stored in RDS
- To scale reads, get more read replicas. Or alternatively, help ElastiCache scale reads by caching information
- Use security groups to restrict traffic between resources

## MyWordPress.com
- Wordpress instance, MySQL, fully scalable
- RDS Multi AZ, or Aurora MySQL Multi AZ, with EC2 auto scaling group
- Aurora has easy Multi AZ and Read Replicas
- EFS with EC2 ENIs more scalable for Wordpress EC2 instances, rather than EBS one per EC2