>Install Redis
```
sudo add-apt-repository ppa:chris-lea/redis-server
sudo apt-get update
sudo apt-get install redis-server
redis-benchmark -q -n 1000 -c 10 -P 5
```
>Configure Redis Master
```
sudo nano /etc/redis/redis.conf
tcp-keepalive 60
bind 172.18.111.11
requirepass 1qa2ws3ed4rf

```
