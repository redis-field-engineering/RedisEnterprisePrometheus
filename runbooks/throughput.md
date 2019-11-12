# Throughput Run Book

## No Redis Requests

### Measurement

```
bdb_total_req < 1
```

### Description

The number of redis operations per second is less than 1

### Escalations

Notify the application support team including the cluster name and BDB number

### Possible Causes

Cause | Check 
--- | ---
Clients misconfigured | Check client configurations
Network firewall | From client attempt to telnet to the DB hostname and port
Host firewall | Ensure the Redis Enterprise hosts allow the DB port to connect


## Excessive Redis Requests

### Measurement

```
bdb_total_req > 1000000

```

### Description

Redis is currently serving over 1M requests/second

### Escalations

Notify the application support team including the cluster name and BDB number

*OR*

Tune the alert to handle a higher than usual number of requests per second


### Possible Causes

Cause | Check 
--- | ---
Application change | Confirm with application support team that the increase is expected

### Remediation Steps

Action | Method 
--- | ---
Tune the threshold up | modify the prometheus rules file and HUP the process
