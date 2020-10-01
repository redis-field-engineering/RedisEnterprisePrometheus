# Nodes Run Book

## Node Not Responding

### Measurement

```
count(node_up) != 3
```

### Description

Ensure we have the expected number of nodes.  This will need to be tuned on a per cluster basis if there are more than 3 nodes.
If you have more than 3 nodes you can modify this alert by cluster name

eg:
```
   - name: nodes
     rules:
     - alert: Node Not Responding
       expr: count(node_up{cluster="redis-prod.example.com"}) != 7
       for: 5m
       labels:
         severity: critical
       annotations:
         description: "Node Down - Cluster: {{ $labels.cluster }} Expected Nodes: 3 Actual: {{$value}}"
         runbook: https://github.com/Redislabs-Solution-Architects/RedisEnterprisePrometheus/blob/master/runbooks/nodes.md
```


### Escalations

Notify the infrastructure support team including the cluster

### Possible Causes

Cause | Check 
--- | ---
Node died | Check node console
Network partition | Check that node can connect over port 9443 to the other cluster nodes


## Node Persistent Storage

### Measurement

```
round(100 * node_persistent_storage_free/node_persistent_storage_avail) <= 5
```

### Description

Less than 5% free disk space remains in the persistent storage partition

### Escalations

Notify the infrastructure support team including the cluster name

### Remediations

Add more disk space or clean out uncessary files not owned by redislabs user on the same disk partition

## Node Ephemeral Storage

### Measurement

```
round(100 * node_ephemeral_storage_free/node_ephemeral_storage_avail) <= 5
```

### Description

Less than 5% free disk space remains in the ephemeral storage partition

### Escalations

Notify the infrastructure support team including the cluster name

### Remediations

Add more disk space or clean out uncessary files not owned by redislabs user on the same disk partition

## Node Free Memory

### Measurement

```
round((100 * node_available_memory/node_free_memory)) <= 15
```

### Description

There is less than 15% free memory available on the Redis Enterpise node

### Escalations

Notify the infrastructure support team including the cluster name

### Remediations

Action | Method 
--- | ---
Migrate shards to different node with free memory | Using rladmin run "migrate shard SHARD target_node NODE" - be sure to migrate proxy if policy is single-node
Add more nodes to the cluster | Add more nodes then migrate shards as detailed above


## Node CPU Usage

### Measurement

```
round(1-node_cpu_idle)*100 >= 80
```

### Description

There is less than 20% free CPU available on the Redis Enterpise node

### Escalations

Notify the infrastructure support team including the cluster name

### Remediations

Action | Method 
--- | ---
Migrate shards to different node with free CPU | Using rladmin run "migrate shard SHARD target_node NODE" - be sure to migrate proxy if policy is single-node
Add more nodes to the cluster | Add more nodes then migrate shards as detailed above
