# Amazon Data Firehose Notes

- Different producers can push records up to 1MB to Firehose
- Optionally, can transform data with Lambda function
- Accumulate data into buffer, which is flushed using batch writes to data destinations
  - S3
  - Redshift
  - OpenSearch
  - 3rd parties like splunk
  - Any HTTPS endpoint
- Fully managed service
- Near real-time

## Kinesis Data Streams vs Data Firehose

- Firehouse has no data storage. It's a way to load streaming data into regular data storage
- Firehouse has no data storage
- Firehouse has automatic scaling, whereas KDS has on-demand mode for auto-scaling.
- Can apply auto-compression for writing to destination