# Capacity Run Book

## DB full

### Measurement

```
bdb_used_memory/bdb_memory_limit
```

### Description

Amount of used memory divided by the memory limit as a percentage.
Current threshold is 98%

### Escalations

Notify the application support team including the cluster name and BDB number

### Possible Causes

Cause | Check 
--- | ---
Possible spike in activity | Check the operations per second graphs in Grafana or Enterprise UI
Database sized incorrectly  | View usage over time

### Remediation Steps

Action | Method 
--- | ---
Increase the database size | In the Redis Enterprise Web UI, click configuration, then edit, then modify Memory Limit setting and save

## DB full in 2 hours

### Measurement

```round(100*(bdb_used_memory/bdb_memory_limit)) < 98 and (predict_linear(bdb_used_memory[15m], 2 * 3600) / bdb_memory_limit) > 0.3 and round(predict_linear(bdb_used_memory[15m], 2 * 3600)/bdb_memory_limit) > 0.98```

### Description

- current usage is greater than 30%
- predictive analysis of the bdb_used_memory projected 2 hours into the future
- is the current DB usage less than 98% (if higher than 98% the DB full alert will fire)

### Escalations

Notify the application support team including the cluster name and BDB number

### Possible Causes

Cause | Check 
--- | ---
Possible spike in activity | Check the operations per second graphs in Grafana or Enterprise UI
Database sized incorrectly  | View usage over time

### Remediation Steps

Action | Method 
--- | ---
Increase the database size | In the Redis Enterprise Web UI, click configuration, then edit, then modify Memory Limit setting and save

### Notes

This is a future alert based on extraplation of the current DB size growth and may require some tuning for your environment
