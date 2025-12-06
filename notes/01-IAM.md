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

## AWS Organizations

- Manage multiple AWS accounts
- One management account, many member accounts
- Consolidate billing for all accounts
- Price benefit from aggregated usage
- Shared reserved instances and saving plan discounts
- API for AWS account creation
- Organizational Units (OU) separate member accounts into groupings, all sitting in root OU with the management account.

### Advantages

- Security of different accounts
- Shared CloudTrail, CloudWatch that is centralised
- Cross-account roles
- IAM policies applied
- Service Control Policies (SCP) are IAM policies that can apply to OU or account for all users/roles, though not applying to management account

### Tag Policies

- Ensure consistent tagging across resources

## IAM Conditions

1. aws:SourceIp - restrict client source IP address API calls
2. aws:RequestedRegion - restrict region API call made to (region of AWS service/resource)
3. ec2:ResourceTag - restrict on tag key-values
4. aws:MultiFactorAuthPresent - force MFA
5. aws:PrincipalOrgID - access must be from an AWS account in the specified AWS organization

## IAM for S3

- Can have bucket level permissions and object level permissions with different actions

## IAM Roles vs Resource Based Policies

- Could use either IAM roles or resource policies to access e.g. S3
- Role makes you give up your original permissions
- However resource policy does not make you give up permissions
- EventBridge will use resource based policies for those services supporting it, and IAM role otherwise

## IAM Permission Boundaries

- Advanced feature that defines maximum permission an IAM user or role can have.
- E.g. the user can have S3 permissions only if the permission boundaries allows S3 permissions, and the user itself has the permission. The user can't have any permissions outside the boundary, even if they're granted
- Can use in combo with organization SCP, organization needs to allow, boundary needs to allow, boundary needs to allow

## IAM Identity Center

- SSO for all AWS accounts on AWS orgs
- Business cloud apps like Salesforce
- Enabled apps and EC2 Windows

## AWS Directory Services

Three versions:

- AWS Managed Microsoft AD. Can trust between on-prem AD and AWS AD
- AD Connector, proxy to on-prem AD, users managed on-prem
- Simple AD, AD-compatible managed director on AWS, but can't be joined with on-prem AD

## AWS Control Tower

- Set up and govern multi-account AWS
- Automate set up, policy management
- Detect policy violations and enact remediations
- Monitor with dashboard

### Guardrails

- Ongoing governance
- Preventative Guardrail - use SCPs
- Detective Guardrail - use AWS Config