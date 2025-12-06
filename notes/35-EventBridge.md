# Amazon EventBridge Notes

- Schedule cron jobs, triggers script in Lambda
- Event pattern, react to event rule
- Trigger lambda, send SQS/SNS

After event from source, EventBridge generates JSON document of event details, can send on to many destinations

- Can also receive events from 3rd party services as well as AWS
- Can also have a Custom Event Bus for custom apps
- Can archive event and replay them