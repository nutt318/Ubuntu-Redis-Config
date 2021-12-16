# Ubuntu-Redis-Config
This guide is for Ubuntu 20.04 and running Redis with multiple instances

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
TimeoutStopSec=0
```
TO:
```
Type=forking
ExecStop=/bin/kill -s TERM $MAINPID
ExecStartPost=/bin/sh -c "echo $MAINPID > /var/run/redis/redis.pid"
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
PIDFile=/run/redis/redis-server.pid
TimeoutStopSec=10
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
### Create directories and update permissions
```
mkdir -p /var/lib/redis_6380
chown -R redis:redis /var/lib/redis_6380
chgrp redis /var/lib/redis_6380
```
### Copy Config and update permissions 
```
cp /etc/redis/redis.conf /etc/redis/redis_6380.conf
chown redis /etc/redis/redis_6380.conf
```
### Edit Config
`vi /etc/redis/redis_6380.conf`

FROM:
```
port 6379
pidfile /var/run/redis/redis-server.pid
logfile /var/log/redis/redis-server.log
dir /var/lib/redis
```
TO:
```
port 6380
pidfile /var/run/redis/redis-server_6380.pid
logfile /var/log/redis/redis-server_6380.log
dir /var/lib/redis_6380
```

### Copy and Setup new Service File
`cp /usr/lib/systemd/system/redis-server.service /usr/lib/systemd/system/redis-server_6380.service`

### Modify Service File to match
`vi /usr/lib/systemd/system/redis-server_6380.service`

FROM:
```
ExecStart=/usr/bin/redis-server /etc/redis/redis.conf
PIDFile=/run/redis/redis-server.pid
```
TO:
```
ExecStart=/usr/bin/redis-server /etc/redis/redis_6380.conf
PIDFile=/run/redis/redis-server_6380.pid
```

### Reload system daemon to update Redis
`systemctl daemon-reload`

### Enable Service at Startup and Check status
```
systemctl enable redis-server_6380
systemctl start redis-server_6380
systemctl status redis-server_6380
```

---
## Setup for additional Instances (if needed)
Start at "Start setup for additional Instances (if needed)"
Replace any mention of 6380 to 6381
