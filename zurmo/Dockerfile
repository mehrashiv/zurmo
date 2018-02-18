FROM ubuntu:16.04

RUN apt-get -y update && apt-get install -y apache2

RUN apt-get update && apt-get install -y php php-mysql php-memcached

RUN apt-get update && apt-get install -y php-curl php-apcu

RUN apt-get update && apt-get install -y php-soap php-imap

RUN apt-get update && apt-get install -y php-gd php-pear

RUN apt-get update && apt-get install -y php-mcrypt php-net-imap php-net-ldap

RUN apt-get update && apt-get install -y libapache2-mod-php php-mbstring

RUN a2enmod deflate

COPY php.ini /etc/php/7.0/apache2/

RUN phpenmod mcrypt && phpenmod imap

COPY zurmo-stable-3.2.3.74732d3df221.tar.gz /var/www/html/

RUN cd /var/www/html/ && tar -xvzf zurmo-stable-3.2.3.74732d3df221.tar.gz && chown root:root -R zurmo && chmod 777 -R zurmo

EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND
