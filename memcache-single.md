> First make sure that all your system packages are up-to-date by running these following apt-get commands in the terminal.
```
sudo apt-get update
sudo apt-get upgrade
```
>Installing Memcached.
```
apt install memcached
```
> Configuration Memcached.
```
nano /etc/memcached.conf
# Default connection port is 11211
-p 11211

systemctl restart memcached
```
>Install Memcached extension for PHP
```
apt-get install php-memcached

# Apache 
systemctl restart apache2

# nginx 
systemctl restart nginx
```
> Test Working
```
#Code For Test
<?php
$mem = new Memcached();
$mem->addServer("127.0.0.1", 11211);
 
$result = $mem->get("blah");
 
if ($result) {
    echo $result;
} else {
    echo "No matching key found yet. Let's start adding that now!";
    $mem->set("blah", "I am data!  I am held in memcached!") or die("Couldn't save anything to memcached...");
}
?>
```
