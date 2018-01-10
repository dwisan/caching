> update the repository and install Apache.
```
apt-get update
apt-get install apache2
```
> Install PHP and Apache's mod_php extension.
```
apt-get install php5 libapache2-mod-php5 php5-mcrypt
```
>Install Memcache Packages
```
apt-get install php5-memcache memcached
```
>Config memcache
```
nano /etc/memcached.conf
-l 1.1.1.1

service memcached restart
```
>Set Memcache as PHP's Session Handler
```
session.save_handler = memcache
session.save_path = 'tcp://1.1.1.1:11211'
```
> restart Apache
```
service apache2 reload
```


