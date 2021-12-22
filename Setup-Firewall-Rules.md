## Run the below commands to allow SSH and access to the Redis default port

### Example: Production running 1 instance
```
ufw allow ssh
ufw allow 6379/tcp
ufw allow from 10.10.1.0/24
ufw allow from 10.10.2.0/24
ufw allow from 10.20.1.0/24
ufw allow from 10.20.2.0/24
ufw allow from 192.168.1.0/24
ufw allow from 172.16.1.0/24
ufw allow from 172.16.2.0/24
ufw allow from 172.16.3.0/24
ufw allow from 172.16.4.0/24
ufw enable
ufw status
```

### Example: Stage running 3 instances
```
ufw allow ssh
ufw allow 6379:6381/tcp
ufw allow from 10.10.1.0/24
ufw allow from 10.10.2.0/24
ufw allow from 10.20.1.0/24
ufw allow from 10.20.2.0/24
ufw allow from 192.168.1.0/24
ufw allow from 172.16.1.0/24
ufw allow from 172.16.2.0/24
ufw allow from 172.16.3.0/24
ufw allow from 172.16.4.0/24
ufw enable
ufw status
```
