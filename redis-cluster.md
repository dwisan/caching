>Install Redis
```
sudo add-apt-repository ppa:chris-lea/redis-server
sudo apt-get update
sudo apt-get install redis-server
redis-benchmark -q -n 1000 -c 10 -P 5
```
>Configure Redis Cluster master nodes
- [x] Redis node master1 (redis-master1.conf)
```
port 6379
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```
- [x] Redis node master2 (redis-master2.conf)
```
port 6380
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```
- [x] Redis node master3 (redis-master3.conf)
```
port 6381
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```
> start redis master server
```
redis-server redis-master1.conf
redis-server redis-master2.conf
redis-server redis-master3.conf
```
> Checking cluster node of Redis
```
redis-cli -h master1 -p 6379 CLUSTER_NODES
redis-cli -h master2 -p 6380 CLUSTER_NODES
redis-cli -h master3 -p 6381 CLUSTER_NODES
```
>form a cluster, the Redis nodes (running in cluster mode)
```
redis-cli -h master1 -p 6379 CLUSTER_NODES MEET master2 6380
redis-cli -h master1 -p 6379 CLUSTER_NODES MEET master3 6381
```
