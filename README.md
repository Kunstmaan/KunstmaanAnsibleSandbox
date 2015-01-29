Ansible Kunstmaan Sandbox
=============================

#####Create a Kunstmaan Sandbox



### Setup

* Mac OS X 10.8.3
* [Vagrant (>= 1.4.3)](http://www.vagrantup.com)
* [VirtualBox (>= 4.3*)](https://www.virtualbox.org)
* Install [Ansible](http://docs.ansible.com)

###### Getting started

* Clone this repository
* import into phpstorm
* install vagrant plugin (https://plugins.jetbrains.com/plugin/7379?pr=idea)
* In PhpStorm - Tools->Vagrant->up or from command line 'vagrant up' from KunstmaanAnsibleSandbox

### Composer will fail - with lack of memory to fix that
* vagrant ssh
* php -d memory_limit=-1 /usr/local/bin/composer update

### Increase Swap size in the vm:
* sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
* sudo mkswap /swapfile
* sudo swapon /swapfile
* sudo /swapfile swap swap defaults 0 0

### Increase memory size in php.ini
* cd /etc/php5/cli

### Give permission to /var/www
* chmod -R 777 /var/www
* cd /var/www/kunstmaan-bundles-standard-edition
* composer install

### Follow instructions on this page
(http://bundles.kunstmaan.be/getting-started/installation)

* sudo apt-get install node
* sudo gem install sass # maybe you need sudo...
* sudo npm install -g bower
* sudo npm install -g grunt
* sudo npm install -g grunt-cli
* sudo npm install -g uglify-js
* sudo npm install -g uglifycss

### check if everything is alright till now:
* php app/check.php

### This part is confusing for those who is installing for the first time:
http://localhost/path/to/app/web/config.php

Note: You can't run this from host YET.

### Stop Nginx server which would be running at 127.0.0.1/8888 from host
* /usr/bin/nginx -s stop

### modify config.php to be allowed to be accessed from host machine
vim /var/www/kunstmaan-bundles-standard-edition/web/config.php

a snippet of config.php
if (!in_array(@$_SERVER['REMOTE_ADDR'], array(
    '127.0.0.1',
    '::1',
'10.0.2.2',
))) {
    header('HTTP/1.0 403 Forbidden');
    exit('This script is only accessible from localhost.');
}

### Continue executing the statements:
app/console kuma:generate:bundle
app/console kuma:generate:default-site --demosite
app/console doctrine:database:create
app/console doctrine:schema:create
app/console doctrine:fixtures:load
app/console kuma:generate:admin-tests

bower install
npm install
sudo grunt build
app/console assets:install web
app/console assetic:dump

### If at any point in these steps you get a DB error, then it can be fixed like this:
sudo /etc/init.d/mysql stop
sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
sudo /etc/init.d/mysql start

select host,user,password from mysql.user;
update mysql.user set password = PASSWORD('root') where user='root' and host=‘localhost’;

MariaDB [(none)]> FLUSH PRIVILEGES;

MariaDB [(none)]> exit

### the way to run this instance is:
on the vm run this:
sudo php -S 0.0.0.0:80

on the host browser
http://127.0.0.1:8888/web/config.php

###complete the steps by clicking on
http://127.0.0.1:8888/web/app_dev.php/_configurator/

if step1 and step2 are followed successfully you should get a yml like this:

http://127.0.0.1:8888/web/app_dev.php/_configurator/final

{ parameters: { database_driver: pdo_mysql, database_host: localhost, database_port: null,
database_name: kunstmaan, database_user: root, database_password: root, mailer_transport: smtp,
mailer_host: 127.0.0.1, mailer_user: null, mailer_password: null, locale: en,
secret: 6352486bf6eafdeb2f04322ac3a7b9baf43bfd15, debug_toolbar: true,
debug_redirects: false, use_assetic_controller: true, requiredlocales: nl|fr|de|en,
defaultlocale: en, multilanguage: true, sentry.dsn: 'https://XXXXXXXX:XXXXXXXX@app.getsentry.com/XXXX',
cdnpath: null, websitetitle: MyProject, session_prefix: myproject, searchport: 9200,
searchindexname: myproject, searchindexprefix: myproject, analytics.googletagmanager: GTM-XXXXXX,
aviary_api_key: 'Register on http://developers.aviary.com/',
google.api.client_id: 'More info at http://bundles.kunstmaan.be/getting-started/advanced/setting-up-the-google-analytics-dashboard"',
google.api.client_secret: null, google.api.dev_key: null, doctrine.server_version: 5.6, database_path: null } }


##### Finally, how to run the admin,
Documentation says this: http://localhost/path/to/app/en/admin
/path/to/app -> /web/app_dev.php/

http://127.0.0.1:8888/web/app_dev.php/en/admin/login

use admin/admin








