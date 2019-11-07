# Utilization Run Book

## Hit ratio is low

### Measurement

```
100*bdb_read_hits/(bdb_read_hits+bdb_read_misses) < 50
```

### Description

Read hit ratio is below 50%.
If you are not using redis in a caching scenario, please disable this check.
You may need to tune the threshold to match your application performance criteria.


### Escalations

Notify the application support team including the cluster and db number

### Possible Causes

Cause | Check 
--- | ---
Application specific | Check application requirements


## Objects Being Evicted from Database

### Measurement

```
bdb_evicted_objects > 1
```

### Description

Keys are being evicted from your database.
In some caching use scenarios this may be acceptable, so please disable this check if you meet such requirements.

### Escalations

Notify the application support team including the cluster and db number

### Remidations 

See (docs)[https://docs.redislabs.com/latest/rs/administering/database-operations/eviction-policy/] on Eviction policy for more information
