# Ubuntu-Redis-Config
This guide is for Ubuntu 20.04 with running Redis and having multiple instances

*Also assums your running at root*

## Check for updates and install
`apt-get update && apt-get upgrade -y`

## Install Redis
`apt-get install redis-server -y`

## Edit default Redis Config file
`vi /etc/redis/redis.conf`
Update the below lines to match
* #bind 127.0.0.1 ::1
* protected-mode no
* databases 50
