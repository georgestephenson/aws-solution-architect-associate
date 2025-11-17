# Amazon ElastiCache Notes

- Managed service for Redis or Memcached
- In-memory databases, high performance, low latency
- Helps reduce DB load
- Helps make apps stateless
- AWS handles OS maintenance, patching, backups, etc

## Redis

- Multi AZ, auto-failover
- Read Replicas
- AOF persistence
- Redis AUTH, extra layer of security

Use case: Gaming leaderboards. Redis Sorted sets guarantee uniqueness and ordering. Realtime leaderboard

## Memcached

- Multi-node for partitioning
- Non persistent
- Backup and restore
- Multi-threaded
- SASL auth

## Patterns

- Lazy Loading, all read data cached, data can become stale
- Write Through, add/update to cache when written to DB (no stale data)
- Session Store - store temporary session data in cache (TTL)


## Important ports to know for exam
Important ports you should probably know. Database ports aren't as important to remember as long as you can tell the difference.

Important ports:

FTP: 21
SSH: 22
SFTP: 22 (same as SSH)
HTTP: 80
HTTPS: 443

vs RDS Databases ports:

PostgreSQL: 5432
MySQL: 3306
Oracle RDS: 1521
MSSQL Server: 1433
MariaDB: 3306 (same as MySQL)
Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)