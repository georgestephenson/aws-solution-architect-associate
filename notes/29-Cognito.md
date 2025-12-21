# Amazon Cognito Notes

- Gives identity to users we don't know
- User Pools: sign in for app users - API gateway, ALB
- Identity Pools: temporary AWS credentials for users to access AWS resources
  - IAM policies for credentials defined in Cognito
  - Authorization not authentication
  - e.g. S3 access tokens for users after they log in
- Cognito for mobile users, hundreds of users

You can have a solution using User Pools and Identity Pools
- Cognito is used as the identity provider to authenticate users (User Pools)
- User Pools returns a JSON Web Token (JWT) for the user
- The JWT is exchanged with the Identity Pool to **issue temporary AWS credentials**

The exam questions can blur the lines between the Cognito services and test you understand the distinction and how they could work together.