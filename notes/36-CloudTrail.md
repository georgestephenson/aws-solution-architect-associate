# AWS CloudTrail Notes

- Auditing of AWS account, enabled by default
- History of events and API calls
- If we want logs for more than 90 days, can send to CloudWatch logs or S3 bucket

## Events

- Management Events: operations performed on AWS resources, e.g. security config, routing data, set up logs
- Data Events: not logged by default, can be high volume, e.g. S3 bucket object-level activity, Lambda function execution
- CloudTrail Insights Events

### CloudTrail Insights Events

- Detect unusual activity:
  - Hitting limits
  - Burst of actions
  - Gaps in maintenance
  - Look for unusual patterns in write events

## Events Retention

- Stored for 90 days
- Could log to S3 and use Athena to keep longer

## EventBridge

- All API calls get logged to CloudTrail. We can use EventBridge to intercept this API call.
- We can set a destination to go from EventBridge into e.g. SNS