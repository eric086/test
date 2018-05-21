FROM ubuntu:16.04
ADD sources.list /etc/apt/sources.list
RUN echo "Asia/Shanghai" > /etc/timezone
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get install -y php-fpm
RUN apt-get -y  install ssh
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN apt-get install -y php-mbstring
RUN apt-get install -y zip unzip
RUN apt-get install -y php-mysql
RUN apt-get install -y php-imagick
RUN apt-get install -y php-redis
RUN apt-get install -y php-intl
RUN apt-get install -y php-curl
RUN apt-get install -y php-xml

RUN rm -rf /var/lib/apt/lists/*
RUN mkdir -p /run/php

ADD default /etc/nginx/sites-available/default
ADD nginx.conf /etc/nginx/nginx.conf
ADD run.sh /run.sh
RUN chmod 755 /run.sh

EXPOSE 80
EXPOSE 443
WORKDIR /var/www/html
CMD ["/run.sh"]
