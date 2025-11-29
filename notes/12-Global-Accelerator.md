# Global Accelerator Notes

## Background 
- Public internet can add lots of latency across the world
- Unicast IP is one server has one IP, Anycast IP, many servers have same IP and user is routed to the nearest one

## How it works 

- Leverage AWS internal network
- 2 Anycast IPs will send traffic to edge locations

## Benefits/Features

- Consistent performance, intelligent routes to lowest latency
- Health Checks
- Fast regional failover
- Security, DDoS protection with AWS Shield

## CloudFront vs Global Accelerator
- CloudFront works with static and dynamic content, content served from edge locations
- Global Accelerator, content still served by application, but proxying packets from edge location, improving performance, good for use cases like gaming (UDP), IoT, Voice over IP