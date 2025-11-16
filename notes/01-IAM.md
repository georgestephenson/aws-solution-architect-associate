# IAM - Identity and Access Management Notes

Root account created by default for AWS account
Create users within your organisation, can be grouped

- User and Groups assigned policies - JSON document
- "Inline" policy - only on user, not inherited from group
- Policies have: effect (allow/deny), principal, actions, resources

Policy JSON for AdministratorAccess, AWS console lists all services allowed. But JSON is simple!

``` JSON
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

### IAM Roles

- Like a user, but roles are only used by AWS services
- e.g. EC2 VM might use a role to access AWS

### IAM Tools

- IAM Credentials Report, Report that lists all users and status
- IAM Access Advisor

### IAM Best Practices

- Don't user root except for AWS account setup
- Users should be in groups, groups should be assigned permissions
- One user per physical person
- Don't share keys
- Grant least privilege (well, this is always true of anything)