FROM eric138520857/ubuntu16.04:basic

MAINTAINER phoenix086@qq.com

RUN apt-get update

RUN apt-get install -y apache2

RUN apt-get install -y php

RUN apt-get install -y libapache2-mod-php

RUN echo "Asia/Shanghai" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

RUN echo "export APACHE_LINSTEN_PORT" >> /etc/apache2/envvars

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

RUN php composer-setup.php

RUN php -r "unlink('composer-setup.php');"

RUN mv composer.phar /usr/local/bin/composer

RUN apt-get install -y php-mbstring

RUN apt-get install -y phpunit

RUN apt-get install -y zip unzip

RUN apt-get install -y php-mysql

RUN apt-get install -y php-imagick

RUN apt-get install -y php-redis

RUN apt-get install -y php-intl

RUN rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

ADD run.sh /run.sh
RUN chmod 755 /*.sh

ADD ports.conf  /etc/apache2/ports.conf
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf

ENV APACHE_LISTEN_PORT 8080
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2

ENV APACHE_DOCUMENT_ROOT /var/www/html

WORKDIR /var/www/html

CMD  ["/run.sh"]
