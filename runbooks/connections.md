# Connections Run Book

## No Redis Connections

### Measurement

```
bdb_conns < 1
```

### Description

Number of redis clients connecting to the database

### Escalations

Notify the application support team including the cluster name and BDB number

### Possible Causes

Cause | Check 
--- | ---
Clients misconfigured | Check client configurations
Network firewall | From client attempt to telnet to the DB hostname and port
Host firewall | Ensure the Redis Enterprise hosts allow the DB port to connect


## Excessive Connections

### Measurement

```
bdb_conns > 64000
```

### Description

Number of redis clients connecting to the database

### Escalations

Notify the application support team including the cluster name and BDB number
*OR*
Tune the number of proxy threads higher in rladmin

### Possible Causes

Cause | Check 
--- | ---
Clients not freeing connections | Check client application configurations

### Remediation Steps

Action | Method 
--- | ---
Increase the number of proxy threads | Using rladmin run "tune proxy PROXY_NUMBER threads VALUE"

### Notes
The current threshold is for default thread count is set for untuned value, so if you up the number of threads modify the alert threshold to match
