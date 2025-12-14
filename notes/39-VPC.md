# Virtual Private Cloud (VPC) Notes

## CIDR IPv4

- Used in Security Group rules and for routing
- Base IP and Subnet Mask

### Subnet Marks

- /32 - allows one IP
- /31 - allows two IP .0 to .1
- /28 - allows 16 IPs ($2^4$), .0 to .15, and so on
- /0 allows all IPs 0.0.0.0 to 255.255.255.255

/24 means last octet can change, /16 last two octets, /8 three octets, /0 all octets

## Public vs Private IP

-  Private IP ranges allowed 
 - 10.0.0.0 - 10.255.255.255 for big networks
 - 172.16.0.0 - 172.31.255.255 used by your AWS default VPC
 - 192.168.0.0 - 192.168.255.255 - typical home network
- All others are Public IPs

## Default VPC

- All accounts have default VPC
- EC2 launched here by default
- EC2 instances will have public IPs in default VPC

## VPC in AWS

- Multiple VPC in region, max 5 per region
- Max 5 CIDRs per VPC, min size /28, max size /16
- Only private IPs allowed
- VPC CIDR shouldn't overlap with other VPCs or on-prem network

## Subnets

- 5 IP addresses reserved in each subnet (first 4 and last 1) not available for EC2 instances
- Subnet can only exist in on Availability Zone (AZ)
- But subnets in different AZ can be in same VPC albeit the VPC must be a single region.

## Internet Gateway (IGW)

- Allows resources, e.g. EC2 instance, in VPC to connect to Internet
- One Internet Gateway : One VPC
- Route tables must also be edited for Internet access to work

## Bastion Hosts

- Users want SSH access to EC2 instance in Private Subnet
- Special EC2 instance called Bastion Host - in Public Subnet
  - Has its own security group, called BastionHost-SG
  - Can access other EC2s in our VPC, even ones in Private Subnet
- Bastion Host must allow public CIDR of your company on port 22, but not open to everything
- Private EC2 instances must allow Bastion Host SG, or the private IP of the Bastion Host

## NAT

- Network Address Translation
- NAT must be in public subnet while instances using it must be in a different subnet with different default routes and route tables, i.e. private subnet.

### NAT Instance (outdated)

- Allows EC2 in private subnet to connect to the Internet
- NAT instance launched in Public Subnet, Elastic IP attached to it
- Route table set to route traffic from private subnet to NAT Instance
- NAT rewrites network packets from external user to proxy requests
- Must disable EC2 source/destination check to allow the network packet rewriting
- Not highly available/resilient, needs an ASG in multi-AZ etc
- Must manage Security Groups and Roles
- Supports port forwarding, Security Groups, can be used as bastion server

### NAT Gateway

- AWS-managed NAT
- High availability, no admin
- Much better than NAT instances
- Created in AZ with Elastic IP
- Must be used by EC2 in a different subnet
- Requires an IGW
- No security group for a NAT gateway, but has a NACL in its subnet.

### Resiliency

- Resilient within one AZ
- Multiple AZs require multiple NAT Gateways

## Security Groups and NACLs (Network Access Control List)

- NACL is stateless, while SG is stateful
- NACL operates at subnet level, whereas SG operates at instance level
- NACL and SG both have inbound and outbound traffic rules
- Assentially SG will remember and allow return traffic while NACL will have rules that always apply
- Like a firewall for traffic to a subnet, covering the subnet
- One per subnet, new subnets assigned the default NACL

## NACL Rules
- First rule match will determine decision

New NACLs deny everything by default. But Default NACL accepts inbound/outbound everything for subnets

## Ephemeral Ports

- Clients connect to server with defined port, and expect response on temporary, ephemeral port, for the duration of that server connection
- For NACLs to allow return traffic, outbound leaving a subnet and inbound entering a subnet, they need allow ALL possible ephemeral ports to/from the subnet CIDRs.

## VPC Peering

- Privately connect two VPCs as if they're the same network
- Can't have overlapping CIDRs
- Not transitive, each VPC needs an explicit connection to communicate with each other VPC
- Can be cross-account and/or cross-region

## VPC Endpoints

- Allow VPCs to connect to AWS services without going through public Internet, but throught the private AWS network
- Instead of a NAT Gateway + Internet Gateway, just use VPC Endpoint to access AWS services from a Private Subnet
- Redundant and scale horizontally

### Types

- Interface Endpoints, powered by PrivateLink. Provisions ENI with private IP address as entry point. Must attach SG. Cost per hour and per GB
- Gateway Endpoints. Provisions gateway, must be used as target in route table. No SG. Supports S3 and DynamoDB. Free

## VPC Flow Logs

- IP traffic info
  - VPC Flow Logs
  - Subnet Flow Logs
  - Elastic network Interface (ENI) Flow Logs
- Can send to S3, CloudWatch Logs, Kinesis Data Firehose
- And captures info from managed interfaces from AWS services too
- Can query logs using Athena
- IAM Service Role for VPC Flow Logs must have permissions in order to publish logs to CloudWatch Logs

### SG and NACL issues

- ACTION field is ACCEPT or REJECT, based on NACL and SG decision

## AWS Site-to-Site VPN

- Allow VPN between the AWS VPC and on-prem corporate network
- Requires a Virtual Private Gateway (VGW) on the AWS side
- Requires Customer Gateway (CGW) - app or physical device on the customer side of the VPN
  - Use public IP if there is one
  - If private, use public IP of the NAT device, if it's enabled for NAT traversal (NAT-T)
- Need to enable **Route Propagation** in Virtual Private Gateway for this to work

## AWS VPN CloudHub

- VPN for multiple customer networks into your VPC
- Low cost hub and spoke model with VPC as the hub
- Then customer networks can communicate with each other
- To set up, have multiple VPN connections on same VGW

## Direct Connect (DX)

- Private connection from remote network to VPC
- Needs private virtual interface between AWS Direct Connect Location, and customer network
- Needs Virtual Private Gateway on VPC
- Access public and private AWS resources
- Use cases: increase bandwidth, more consistent network as it's private, hybrid cloud and on-prem environment

### Direct Connect Gateway

- Connect to many VPCs in different regions within same account
- But for max resiliency, can have more than one connection to each customer network

### Connection types

1. Dedicated connection, physical ethernet port
2. Hosted connection, via AWS Direct Connect Partners

Lead times often longer than 1 month to estable a Direct Connect connection

### Direct Connect and Site-to-Site VPN

- Could have site-to-site VPN through public Internet as a backup option for the Direct Connect which is the more expensive option. You might not want to pay for a 2nd Direct Connect that is only for the backup option.

## Transit Gateway

- Transitive peering, between thousands of VPCs and on-prem networks, using hub-and-spoke connection
- Reduces complexity of network topologies need for direct VPC peering
- Can connect Direct Connect Gate or VPN Gateway-Customer Gateway into the Transit Gateway
- Can work cross-region, cross-account. Can peer Transit Gateways across regions
- Support IP Multicast, only AWS networking service that does so

### Site-to-site VPN ECMP (Equal-cost multi-path routing)

- Forward packet over multiple best paths
- Can add more tunnels to your customer network

## Traffic Mirroring

- Capture and inspect network traffic, without impacting/slowing down traffic
- Specify ENIs traffic comes from and ENIs or NLB to mirror traffic to
- Capture all packets or just some filtered ones

## IPv6

- EC2 instance gets a private IPv4 and a public IPv6 by default

### Egress-only Internet Gateway

- Similar to NAT Gateway for IPv6
- Allow outbound over IPv6 while preventing inbound IPv6
- Must update Route Tables

## Networking Costs

- In one AZ, free traffic into EC2, free private traffic between EC2
- Between AZ, charges, twice as much if public
- Inter-region traffic more expensive
- Use private IP for better performance and savings
- Egress traffic usually has cost, try to minimise egress

### S3 Data Transfer Pricing

- S3 ingress free
- S3 to internet 9 cents per GB
- S3 Transfer Acceleration - add 4 to 8 cents per GB
- S3 to CloudFront free
- CloudFront to Internet cheaper per GB

## AWS Network Firewall

- Protect entire VPC, Layer 3 to Layer 7, internet, VPC to VPC, or Direct Connect, or Site-to-Site VPN
- Uses AWS Gateway Load Balancer
- Rules centrally applied, apply to many VPCs
- Support lots of rules, IPs, protocal, domain list rules, regex patterns, traffic filtering
- Send logs to usual log services, S3, CloudWatch Logs, Kinesis Data Firehose

## VPC Sharing

- AWS accounts can share one or more subnets using VPC sharing, part of Resource Access Manager