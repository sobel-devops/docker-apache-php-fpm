# docker-apache-php-fpm
stack apache and php with fpm.

This two projects help for connecting the apache http server with fpm server which execute php code.

## build images
docker build -t sobel/php-fpm .
docker build -t sobel/apache-fpm .

images are in docker hub via link  https://hub.docker.com/u/fallphenix


### running

creating network for the stack
```
docker network create infra-net
```
running the fpm server with alias name "php-fpm-host" for apache to connect in this
```
docker run -d  -p 9000:9000 --network infra-net --network-alias php-fpm-host --name php-fpm   sobel/php-fpm
```
running the apache server with sites-enabled folder : 

```
docker run -d   -p 80:80 --network infra-net -v path-to\sites-enabled:/etc/apache2/sites-enabled   --name apache-fpm   sobel/apache-fpm
```

sites-enabled folder 

000-default.conf
```
<VirtualHost *:80>
    DocumentRoot /var/www/html
 
    <Directory /var/www/html>
        Options -Indexes +FollowSymLinks +MultiViews
        AllowOverride All
        Require all granted
    </Directory>
 
    <FilesMatch \.php$>
        # 2.4.10+ can proxy to unix socket
        #SetHandler "proxy:unix:/run/php/php-fpm.sock|fcgi://127.0.0.1:9000"

         SetHandler "proxy:fcgi://php-fpm-host:9000"
    </FilesMatch>
 
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

then go to : http://localhost/index.php
