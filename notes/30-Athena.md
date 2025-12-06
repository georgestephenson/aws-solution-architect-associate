# Amazon Athena Notes

- Serverless query service for S3 data
- Use SQL language
- Support CSV, JSON, Parquet, others
- Use with Quicksight for reporting/dashboards
- Exam tip: serverless analysis of S3 with SQL - use Athena
- Columnar data has cost saving and performance improvement
- Therefore **Parquet** or **ORC** recommended formats
- Service called "Glue" can convert data formats

## Federated Query

- SQL queries across AWS or on-premises data sources, using Data Source Connectors which run on Lambda functions