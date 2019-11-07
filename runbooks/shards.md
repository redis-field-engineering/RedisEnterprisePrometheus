# Shards Run Book

## Shard CPU usage is excessive

### Measurement

```
redis_process_cpu_usage_percent >= 80
```

### Description

A shard is using more than 80% of CPU

### Escalations

Notify the infrastructure support team including the cluster

### Possible Causes

Cause | Check 
--- | ---
Hot key | Check that there is not a hot key on this shard
Insufficient sharding | Shard out your database further


## Hot Master Shard

### Measurement

```
redis_process_cpu_usage_percent{role="master"} > 0.75 and redis_process_cpu_usage_percent{role="master"} > on (bdb) group_left() (avg by (b  db)(redis_process_cpu_usage_percent{role="master"}) + on(bdb) 1.2 * stddev by (bdb) (redis_process_cpu_usage_percent{role="master"}))
```

### Description

One of multiple master shards is consuming much more CPU than the other shards

### Escalations

Notify the infrastructure support team including the cluster

### Possible Causes

Cause | Check 
--- | ---
Hot key | Check that there is not a hot key on this shard
Insufficient sharding | Shard out your database further


## Master Shard down


### Measurement

```
redis_master_link_status{role="slave"} < 1.0
```

### Description

There is a slave shard in the cluster that does not have a master and is unable to be promoted

### Escalations

Contact Redislabs Support team and upload a debug package
