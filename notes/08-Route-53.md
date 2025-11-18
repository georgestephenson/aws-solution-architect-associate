# Amazon Route 53 Notes

## What is DNS?

- Domain Name System - domain names, URLs, mapped to IPs
- DNS has hierarchy, with the prefix and suffix www. and .com
- Domain Registrar
- DNS Records
- Zone File containing DNS Records
- Name Server resolves DNS queries
- TLD .com, etc.
- SLD amazon.com, etc.

Web browser talks to Local DNS server
which talks to root DNS to get TLD
then talk to TLD DNS to get SLD
then talk to SLD DNS to get IP
then cache and return IP

## What is Amazon Route 53?

- Managed DNS, highly available, scalable
- Authoritative - you can update DNS
- 53 is the traditional DNS port
- Most know record types: A, AAAA, CNAME, NS
  - A - maps hostname to IPv4
  - AAAA - maps hostname to IPv6
  - CNAME - maps hostname to another hostname
  - NS - name servers for hosted zone

## Hosted Zone

- Container for records that define how to route traffic
- Public Hosted Zones for public domains, resources with public IPs.
- Private Hosted Zone for private VPC. Can identify resources within VPC with private IPs.

## Records TTL (Time To Live)

- Cache in client for duration of TTL - cache the IP for that DNS so we don't need to query each time

High TTL e.g. 24 hours, less traffic, but potentially outdated
Low TTL e.g. 60 seconds, more traffic, but record less outdated, easy to change records

TTL is mandatory except for Alias records

## CNAME vs Alias
### CNAME
- CNAME only works for non-root domain e.g. something.mydomain.com not www.mydomain.com
### ALIAS
- Alias points hostname to AWS resource, works for root or non-root domains. Free of charge, native health check capability
- Extension of DNA in Route 53
- Targets: Elactic Load Balancers, CloudFront Distributions, API Gateway, Elastic Beanstalk, S3 Websites, etc etc
- You can't set ALIAS for EC2 DNS
- Always A or AAAA record

## Health Checks
- HTTP Health Checks are for public records
- Automated DNS Failover
- 15 global health checkers will check around the world, if >18% report healthy, endpoint is considered healthy
- Calculated health check - combine child health checks and specify how many need to pass to make parent health check pass
- Health checks can't access private VPC endpoints, but can create a CloudWatch metric with an alarm, then Health Check can check the alarm

## Routing Policies

Several different routing policies as follows

### Simple
- Route traffic to one resource/IP, if many returned, client randomly chooses one

### Weighted
- Control % of requests going to each resource
- Use case: load balancing, A/B testing different versions of an application

### Latency-based

- Redirect to resource with lowest latency for the user

### Failover

- primary and secondary resources e.g. primary EC2 and secondary. If health check fails on primary, can failover to secondary disaster recovery EC2

### Geolocation

- Based on user location - Continent, Country or US State, using most precise location
- Should have a default set
- Use case: localisation

### Geoproximity

- Based on geographic location of users
- But can shift more traffic to location based on "bias" value set

### IP-based

- Based on client IP
- Provide list of CIDRs to match client IPs, and corresponding endpoints
- Optimise performance, reduce network costs, due to knowing specific ISP to route to specific endpoint

### Multi Value

- Multiple resources returned
- Client-side load balancing
- Associate each with health checks which would exclude if not healthy
- Client randomly chooses one IP 

## Domain Registrar vs. DNS Service
- Can register with any domain registrar, usually provide a DNS service
- But can use any DNS server, if we specify the nameservers in e.g. GoDaddy
- So could use Route 53 for most custom domain names purchased from other registrars

## Hybrid DNS

- Between VPC and networks

## Resolver Endpoint

- Resolvers help go from e.g. private on-premises to AWS VPC, using inbound or vice versa outbound resolver endpoints