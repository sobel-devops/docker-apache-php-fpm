FROM php:7.2.33-fpm
RUN apt-get update && apt-get install -y build-essential libmcrypt-dev libicu-dev libzip-dev zlib1g-dev 
RUN apt-get install -y  libssl-dev libpng-dev libjpeg-dev libfreetype6-dev libonig-dev
RUN apt -y install iputils-ping
RUN apt -y install telnet
RUN docker-php-ext-install intl json zip gd mbstring  pdo pdo_mysql mysqli iconv 
COPY ./www/ /var/www/html
COPY ./php-fpm.d/ /usr/local/etc/php-fpm.d
USER www-data
EXPOSE 9000