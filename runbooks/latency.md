# Latency Run Book

## Average Latency

### Measurement

bdb_avg_latency

### Description

Average latency of operations on the database from the time the request hits the Enterprise proxy until the request is returned. Measured in seconds

## Escalations

Notify the application support team including the cluster name and BDB number

## Possible Causes

Cause | Check 
--- | ---
Possible spike in activity | Check the operations per second graphs in Grafana or Enterprise UI
Slow running queries | Check the slow log in the Redis Enterprise UI for the database

## Remediation Steps

Action | Method 
--- | ---
Increase the number of database shards to handle the load | The database can be scaled up online by going to the Web UI and enabling clustering on the database
Work with application team to write more performant queries | Developers can fetch the slow log with the cli.  redis-cli -h HOST -p PORT -a PASSWORD SLOWLOG GET 100