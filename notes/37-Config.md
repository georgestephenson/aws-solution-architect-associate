# AWS Config Notes

- Audit and record compliance of AWS resources
- Can set rules on config e.g. do any buckets have public access, then get alerts via SNS for changes to these
- Per-region service, aggregate across regions
- Can store in S3 fro analysis in Athena
- Managed AWS config rules, and custom config rules, defined in Lambda
- No free tier

## Remediation

- Automate remediation of non-compliance with SSM Automation Document, to trigger some action