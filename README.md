# Redis 1 Master 2 Slave

## Redis Master Server Config File
```
bind 0.0.0.0
protected-mode yes
port 6379 
tcp-keepalive 60
pidfile /var/run/redis_6379.pid
replica-read-only yes
requirepass admin
appendonly yes
appendfilename "appendonly.aof"
appendfsync everysec
```

## Redis slave Server Config File
```
bind 0.0.0.0
protected-mode yes
port 6379 
tcp-keepalive 60
pidfile /var/run/redis_6379.pid
replicaof <masterip> <masterport>
masterauth admin
requirepass admin
replica-read-only yes
appendonly yes
appendfilename "appendonly.aof"
appendfsync everysec
```

## Deploy Redis Cluster 3 master 3 slave

```
# docker-compose up -d redis-m1
# docker-compose up -d redis-m2
# docker-compose up -d redis-m3
```

## Test Connect Master
```
# docker-compose exec redis-m1 bash
# redis-cli -h 127.0.0.1 -p 6379 -a admin
> info replication
> set hello 'world'
> get hello
```

## Test Connect Slave
```
# docker-compose exec redis-m2 bash
# redis-cli -h 127.0.0.1 -p 6380 -a admin
> (error) READONLY You can't write against a read only replica.
> slaveof no one
> slaveof 127.0.0.1 6379
```
### Reference
> https://www.tecmint.com/setup-redis-cluster-in-centos-8/

> https://redis.io/topics/cluster-tutorial

> https://www.linode.com/docs/guides/how-to-install-and-configure-a-redis-cluster-on-ubuntu-1604/

### Refernce 1 Master 2 Slave
> https://www.digitalocean.com/community/tutorials/how-to-configure-redis-replication-on-ubuntu-16-04

> https://curiousviral.com/configure-redis-master-and-slave/


#   R e d i s - M a s t e r - S l a v e  
 