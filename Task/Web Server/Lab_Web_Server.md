# I. Topology
## Server 1: MySQL</br>
IP: 192.168.1.1
## Server 2: Install Apache, PHP, WordPress
IP 192.168.1.2
# II. Installation
## Server 1
**192.168.1.1**
### Step 1: Install MySQL
```sh
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum install mysql-server
systemctl start mysqld
```
**Config MySQL**
```
mysql_secure_installation
```
### Step2: Create Databases 
```
create database name-database;
create user 'user'@'IP' identified by 'password';
grant all privileges on name-database to 'user'@'IP';
flush privileges;
exit
```
**Example:**
```
create database wordpress;
create user 'user1'@'192.16.1.2' identified by 'password';
grant all privileges on name-database to 'user'@'192.168.1.2';
flush privileges;
exit
```
## Server 2:
**IP: 192.168.1.2**
### Step 1: Install Apache
```sh
yum install httpd -y
```
**Config httpd**
```sh
systemctl start httpd
systemctl enable httpd
```
### Step 2: Install PHP
```sh
yum install php php-mysql php-gd php-pear –y
systemctl restart httpd
```
### Step 3: Install WordPress
```sh
cd /var/www/html/
mv wordpress/* /var/www/html/
cp wp-config-sample.php wp-config.php
```
**Config file **wp-config.php**
```sh
vim wp-config.php

define('DB_NAME', 'database_name_here');    
define('DB_USER', 'username_here');    
define('DB_PASSWORD', 'password_here');      
define('DB_HOST', 'localhost'); 
```

**Example**
```sh
vim wp-config.php

define('DB_NAME', 'wordpress');    
define('DB_USER', 'user1');    
define('DB_PASSWORD', 'password');      
define('DB_HOST', '192.168.1.1'); 
```