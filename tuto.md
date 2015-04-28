#Installation serveur

##Ajout des sources

Dans /etc/sources.list

deb http://packages.dotdeb.org wheezy all

deb-src http://packages.dotdeb.org wheezy all

deb http://packages.dotdeb.org wheezy-php55 all

deb-src http://packages.dotdeb.org wheezy-php55 all

deb http://download.webmin.com/download/repository sarge contrib

deb http://webmin.mirror.somersettechsolutions.co.uk/repository sarge contrib

deb http://nginx.org/packages/mainline/debian/ wheezy nginx

deb-src http://nginx.org/packages/mainline/debian/ wheezy nginx

wget http://www.dotdeb.org/dotdeb.gpg

apt-key add dotdeb.gpg

wget http://www.webmin.com/jcameron-key.asc

apt-key add jcameron-key.asc

wget http://nginx.org/keys/nginx_signing.key

apt-key add nginx_signing.key

apt-get clean && apt-get update && apt-get upgrade

##Packages divers

apt-get install curl

apt-get install git

apt-get install imagemagick

wget http://downloads.sourceforge.net/project/wkhtmltopdf/0.12.2.1/wkhtmltox-0.12.2.1_linux-wheezy-amd64.deb

(Attention il faut réécrire le -i)

dpkg –i wkhtmltox-0.12.2.1_linux-wheezy-amd64.deb

apt-get -f install

(bin dans /usr/local/bin)

apt-get install fail2ban

apt-get install webmin

##Installation sudo

apt-get install sudo

ajout utilistaeurs par :

visudo

##Mdifier la config ssh

vi /etc/ssh/sshd_config

changer Port

modifier PermitRootLogin à no

AllowUsers <user1> <user2> …

redemarrer ssh :

/etc/init.d/ssh restart

##Installation nginx

apt-get install nginx

###Configuration

[voir](https://bitbucket.org/Grosloup/tuto-server-howto/src/6b1ea32d51efa0fbbd4aae51c2344b73ab9a1df6/config-nginx.md?at=master)

##Installation mysql

apt-get install mysql-client mysql-server mysql-common

puis :

mysql_secure_installation

###Creation base de données

CREATE DATABASE [dbname] CHARACTER SET 'utf8' COLLATE 'utf8_general_ci';

###Ajout utilisateurs et droits

CREATE USER '[username]'@'localhost' IDENTIFIED BY '[password]';

GRANT ALL PRIVILEGES ON [dbname].* TO '[username]'@'localhost;

###Optimisation

my.conf

[client]

default-character-set = utf8


[mysqld]

character_set_client=utf8

character_set_server=utf8

collation_server = utf8_general_ci

key_buffer = 32M

max_allowed_packet = 16M

query_cache_limit = 2M

query_cache_size = 32M

slow_query_log = 1

slow_query_log_file = /var/log/mysql/mysql-slow.log

long_query_time  = 2

###Dump et sync

TODO

##Installation php5

apt-get install php5-fpm php5-cli php5-dev php-pear php5-curl php5-gd php5-imap php5-intl php5-mcrypt php5-sqlite php5-xmlrpc php5-xsl php5-imagick php5-mysql php5-apcu

###modif php.ini (fpm, cli)

upload_max_filesize = 8M

default_charset = "UTF-8"

date.timezone=Europe/Paris 

###Ajout xdebug

pecl install xdebug

puis dans php.ini :

zend_extension=/usr/lib/php5/20121212/xdebug.so

[XDEBUG]

xdebug.remote_connect_back=1

xdebug.default_enable=1

xdebug.remote_autostart=0

xdebug.remote_enable=1

xdebug.var_display_max_data=-1

xdebug.var_display_max_children=-1

xdebug.var_display_max_depth=-1

xdebug.max_nesting_level=250

xdebug.remote_port=9000

xdebug.remote_handler=dbgp

###Optimisation php

TODO

##ELK

[voir](https://github.com/Grosloup/tuto-elk-howto/blob/master/tuto.md)

##Iptabales

cd /etc/init.d

wget https://bitbucket.org/Grosloup/tuto-server-howto/src/ee285dc639b7bae54457ca813e663fe14f44319f/firewall?at=master
