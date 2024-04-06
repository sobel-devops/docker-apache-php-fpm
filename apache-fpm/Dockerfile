FROM debian:stable
RUN apt-get -y update
RUN apt -y install apache2 
RUN apt -y install iputils-ping
RUN apt -y install telnet
RUN a2dismod mpm_prefork
RUN a2enmod mpm_event
RUN a2enmod rewrite
RUN a2enmod remoteip
RUN a2enmod alias proxy proxy_fcgi
RUN chown -R www-data:www-data /var/www
RUN mkdir -p /var/run/apache2
RUN mkdir -p /var/log/apache2
RUN chown -R www-data:www-data /var/run/apache2
RUN chown -R www-data:www-data /var/log/apache2
USER www-data
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]
EXPOSE 80 443 