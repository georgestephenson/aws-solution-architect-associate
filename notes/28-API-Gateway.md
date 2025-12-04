# AWS API Gateway Notes

- Serverless REST API
- Proxy requests to Lambda: no infrastructure
- API versioning
- Multiple environments
- Security
- API keys, request throttling
- Swagger / OpenAPI
- Request/response middleware
- Cache API responses

Can redirect to Lambda function, or HTTP, or any AWS service

## Endpoint Types

- Edge-Optimized (default): routed through edge locations, though gateway in only one region
- Regional: one region, could manually combine with CloudFront for more control
- Private: own VPC