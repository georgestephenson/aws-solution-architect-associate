# Reshift Notes

- OLAP analytics database, not OTLP
- 10x better performance than other data warehouses
- Columnar storage instead of row-based
- Modes: Provisioned cluster or Serverless cluster
- SQL interface
- BI tools: Quicksight, Tableau

## Cluster

- Has a leader node to do query planning, and compute nodes to perform queries in parallel and send results to leader. Leader than aggregates results from compute nodes.

## Snapshots

- Point-in time backups, stored in S3, can restore snapshot into a new cluster.

## Load data

- Kinesis Data Firehose
- Copy from S3 bucket directly
- EC2 instance

## Redshift Spectrum

- Query data in S3 without loading into Redshift.
- Work is done by 1000s of Redshift Spectrum Nodes on S3