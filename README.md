# Ubuntu-Redis-Config
This guide is for Ubuntu 20.04 with running Redis and having multiple instances

*Also assums your running at root*

### Check for updates and install
`apt-get update && apt-get upgrade -y`

### Install Redis
`apt-get install redis-server -y`

### Edit default Redis Config file
`vi /etc/redis/redis.conf`
Update the below lines to match
* #bind 127.0.0.1 ::1
* protected-mode no
* databases 50

### Edit redis-server.service file
`vi /usr/lib/systemd/system/redis-server.service`
FROM:
```
Type=forking
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
PIDFile=/run/redis/redis-server.pid
```
TO:
```
Type=forking
ExecStop=/bin/kill -s TERM $MAINPID
ExecStartPost=/bin/sh -c "echo $MAINPID > /var/run/redis/redis.pid"
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
PIDFile=/run/redis/redis-server.pid
```
### Reload system daemon to update Redis
`systemctl daemon-reload`

### Restart Redis and check if service is running
`systemctl status redis`

### Test Redis Connectivity
`redis-cli ping`
Should receive `PONG`


---
## Start setup for additional Instances (if needed)
`mkdir -p /var/lib/redis_6380`
`chown -R redis:redis /var/lib/redis_6380`
`chgrp redis /var/lib/redis_6380`


`cp /etc/redis/redis.conf /etc/redis/redis_6380.conf`
`chown redis /etc/redis/redis_6380.conf`
