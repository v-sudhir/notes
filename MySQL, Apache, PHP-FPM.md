Install php 8.0, apache, mysql server and memcached on CentOS 8
```bash
# Enable Fastmirror
vi /etc/yum.conf
fastestmirror=1
max_parallel_downloads=8

yum install epel-release
yum update -y

yum module reset php
yum module enable php:8.0
```

```bash
# Install default packages
yum install php-opcache php-sodium php-pear.noarch php-pdo php-mysqlnd php-mbstring php-intl php-json php-fpm php-devel php-cli php-bcmath php-pecl-zip httpd memcached mysql-server

# install composer
export COMPOSER_RUNTIME_ENV=virtualbox

# Install php-memcached extension
yum install zlib-devel fastlz-devel libevent-devel libcurl-devel libxml2-devel libzstd libmemcached-devel
```
```bash
pecl install igbinary
echo "extension=igbinary.so" > /etc/php.d/40-igbinary.ini

pecl install msgpack
echo "extension=msgpack.so" > /etc/php.d/40-msgpack.ini

pecl install redis
echo "extension=redis.so" > /etc/php.d/40-redis.ini

pecl install memcached
echo "extension=memcached.so" > /etc/php.d/50-memcached.ini

# auto start services
systemctl enable php-fpm mysqld httpd memcached
systemctl start php-fpm mysqld httpd memcached
```
```bash
# set password
mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'Mysql.123';
# Add apache user to vbox user
usermod -a -G vboxsf apache
```
```cnf
vi /etc/my.cnf
#for mysql 8 with 1GB Ram

# Data Storage
datadir = /var/lib/mysql

# Networking
bind-address = 0.0.0.0
interactive_timeout = 10
wait_timeout = 10
skip-name-resolve

# InnoDB Storage Engine
default_storage_engine = InnoDB
innodb_buffer_pool_size = 128M
innodb_flush_log_at_trx_commit = 2
innodb_flush_method = O_DIRECT
innodb_log_buffer_size = 8M
innodb_log_file_size = 32M
innodb_thread_concurrency = 0

# Connection and Thread Settings
max_connections = 50
thread_cache_size = 4
thread_stack = 192K

# Temp Tables
tmp_table_size = 32M
max_heap_table_size = 32M

# Performance and Memory
table_open_cache = 64
max_allowed_packet = 16M
sort_buffer_size = 512K
read_buffer_size = 256K
read_rnd_buffer_size = 512K
myisam_sort_buffer_size = 8M
thread_stack = 192K

# Temporary Files
tmpdir = /tmp

# Character Sets
character_set_server = utf8mb4
collation_server = utf8mb4_unicode_ci

# InnoDB Settings
innodb_file_per_table = 1
innodb_flush_neighbors = 0

# Additional Settings
innodb_doublewrite = 0
skip_external_locking

# Logging
general_log = 1
general_log_file = /var/log/mysql/general.log
slow_query_log = 1
long_query_time = 5
slow_query_log_file = /var/log/mysql/mysql-slow.log

# Others
max_connect_errors  = 1000000
```
CentOS 9 Apache
```bash
vi /etc/httpd/conf/httpd.conf
EnableSendfile Off
```
On Ubuntu
```bash
sudo apt-get install virtualbox-guest-additions-iso
sudo apt install build-essential dkms
mount /usr/share/virtualbox/VBoxGuestAdditions.iso /mnt

sudo apt install php7.2-fpm php7.2-common php7.2-mysql php7.2-xml php7.2-xmlrpc php7.2-curl php7.2-gd php7.2-cli php7.2-dev php7.2-mbstring php7.2-soap php7.2-zip php7.2-bcmath php7.2-zip php7.2-tidy php7.2-opcache php7.2-intl php7.2-pear php7.2-solr php7.2-memcached php7.2-igbinary php7.2-msgpack apache2 

# Enable Apache Event module.
a2enmod actions headers rewrite mpm_event proxy_fcgi setenvif

# Now you can enable PHP-FPM configuration. 
a2enconf php7.2-fpm

# Create a new Apache vhost configuration. 
sudo nano /etc/apache2/sites-available/domain.conf



# Now you can enable the new Apache configuration. 
sudo a2ensite domain.conf
usermod -a -G vboxsf www-data
```
