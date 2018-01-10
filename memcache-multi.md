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

#host 1
-l 1.1.1.1

#host 2
-l 2.2.2.2

#host 3
-l 3.3.3.3

service memcached restart
```
>Set Memcache as PHP's Session Handler
```
session.save_handler = memcache
session.save_path = 'tcp://1.1.1.1:11211,tcp://2.2.2.2:11211,tcp://3.3.3.3:11211'
```
>Configure Memcache for Session Redundancy
```
memcache.allow_failover=1
memcache.session_redundancy=4
```
> restart Apache
```
service apache2 reload
```
>Test Session Redundancy
```
<?php
    header('Content-Type: text/plain');
    session_start();
    if(!isset($_SESSION['visit']))
    {
        echo "This is the first time you're visiting this server\n";
        $_SESSION['visit'] = 0;
    }
    else
            echo "Your number of visits: ".$_SESSION['visit'] . "\n";

    $_SESSION['visit']++;

    echo "Server IP: ".$_SERVER['SERVER_ADDR'] . "\n";
    echo "Client IP: ".$_SERVER['REMOTE_ADDR'] . "\n";
    print_r($_COOKIE);
?>
```
