# docker-apache-php-fpm
stack apache and php with fpm.

This two projects help for connecting the apache http server with fpm server which execute php code.

## build images
docker build -t sobel/php-fpm .
docker build -t sobel/apache-fpm .

images are in docker hub via link  https://hub.docker.com/u/fallphenix


### running

docker network create infra-net
docker run -d  -p 9000:9000 --network infra-net --network-alias php-fpm-host --name php-fpm   sobel/php-fpm
docker run -d   -p 80:80 --network infra-net -v D:\dev\containerisation\daarapps\sites-enabled:/etc/apache2/sites-enabled   --name apache-fpm   sobel/apache-fpm

then go to : http://localhost/index.php