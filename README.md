### To install apache
~~~
apt update
apt install apache2 -y
~~~

### To install php
~~~
sudo apt install -y php php-curl libapache2-mod-php php-mbstring php-xmlrpc php-soap php-gd php-xml php-cli php-zip php-bcmath php-tokenizer php-json php-pear
~~~
### To install composer
~~~
curl -sS https://getcomposer.org/installer | php 
sudo mv composer.phar /usr/local/bin/composer 
~~~
~~~
cd /var/www/html
~~~

### To create project
~~~
composer create-project laravel/laravel <your_project_name_here>
~~~
~~~
cd <your_project_name_here>
~~~
~~~
chown www-data:www-data * -R
chown www-data:www-data .* -R
~~~

### to create apache configuration file
~~~
cd /etc/apache2/sites-available
~~~
~~~
vi laravel.conf
~~~
~~~
<VirtualHost *:80>
    ServerName domainname.com

    DocumentRoot /var/www/html/<your_project_name_here>/public

    <Directory /var/www/html/<your_project_name_here>>
        AllowOverride All
        Order allow,deny
        Allow from all
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/my_project_error.log
    CustomLog ${APACHE_LOG_DIR}/my_project_access.log combined
</VirtualHost>
~~~
~~~
a2dissite 000-default.conf
a2ensite laravel.conf
~~~
~~~
service apache2 restart
~~~
