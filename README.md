# laravel-apache2-setup
laravel apache2 ubuntu server setup

apt-get update

apt-get install apache2

systemctl start apache2

apt-get install python-software-properties

add-apt-repository ppa:ondrej/php

apt-get update

apt install php7.1 php7.1-xml php7.1-mbstring php7.1-mysql php7.1-json php7.1-curl php7.1-cli php7.1-common php7.1-mcrypt php7.1-gd libapache2-mod-php7.1 php7.1-zip


curl -sS https://getcomposer.org/installer | php

mv composer.phar /usr/bin/composer

composer create-project laravel/laravel /var/www/html/laravel

nano /etc/apache2/sites-available/000-default.conf
## add following lines
DocumentRoot "/var/www/html/laravel/public"

    CustomLog       /var/www/html/laravel/access.log common
    ErrorLog        /var/www/html/laravel/error.log    

   <Directory /var/www/html/laravel/public>
      <IfModule mod_rewrite.c>
       Options -MultiViews
       RewriteEngine On
       RewriteCond %{REQUEST_FILENAME} !-f
       RewriteRule ^ index.php [L]
      </IfModule>
   </Directory>

systemctl restart apache2

chown -R www-data:www-data /var/www/html/laravel

chmod -R 755 /var/www/html/laravel/storage

