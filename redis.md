>Installing the Redis Server
```
sudo apt-add-repository ppa:chris-lea/redis-server
sudo apt-get update
sudo apt-get install redis-server
```
>Installing the Redis Client and PHP Extension
```
sudo apt-get update
sudo apt-get install redis-tools php-redis
```
>Configure Redis to Accept External Connections
```
sudo nano /etc/redis/redis.conf
      bind localhost 172.18.111.10
sudo service redis-server restart
```
>Set a Password for the Redis Server
```
sudo nano /etc/redis/redis.conf
      requirepass 1qa2ws3ed4rf
sudo service redis-server restart
```
>Test Redis Connection and Authentication
```
redis-cli -h 172.18.111.10
Output
172.18.111.10:6379>
172.18.111.10:6379> AUTH 1qa2ws3ed4rf
172.18.111.10:6379> keys *
```
>Install the Redis Extension on the Web Server
```
sudo apt-get update
sudo apt-get install php5-redis
```
>Set Redis as the Default Session Handler on the Web Server
```
# On LAMP environments:
sudo vim /etc/php5/apache2/php.ini

#On LEMP environments:
sudo vim /etc/php5/fpm/php.ini

session.save_handler = redis
session.save_path = "tcp://172.18.111.10:6379?auth=1qa2ws3ed4rf"

#On LAMP environments:
sudo service apache2 restart

#On LEMP environments:
sudo service php5-fpm restart 

```
>Test Redis Session Handling
#Code Testing
```
<?php
 session_start();
 $count = isset($_SESSION['count']) ? $_SESSION['count'] : 1;
 echo $count;
 $_SESSION['count'] = ++$count;
>
```
# Check session in redis server
```
$ redis-cli -h 172.18.111.10
172.18.111.10:6379>
172.18.111.10:6379> AUTH 1qa2ws3ed4rf
172.18.111.10:6379> keys *
```
