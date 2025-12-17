# Amazon Cognito Notes

- Gives identity to users we don't know
- User Pools: sign in for app users - API gateway, ALB
- Identity Pools: temporary AWS credentials for users to access AWS resources
  - IAM policies for credentials defined in Cognito
  - Authorization not authentication
  - e.g. S3 access tokens for users after they log in
- Cognito for mobile users, hundreds of users