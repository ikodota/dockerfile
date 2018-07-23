FROM php:7.2.2-fpm-alpine3.7
LABEL maintainer="php-composer Docker Maintainers <ikodota@gmail.com>"

#安装composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
php composer-setup.php && \
php -r "unlink('composer-setup.php');" && \
mv composer.phar /usr/local/bin/composer && \
composer self-update


#配置php
RUN sed -i -e 's/listen = 127.0.0.1:9000/listen = 9000/g' /usr/local/etc/php-fpm.d/www.conf
RUN sed -i -e 's/;daemonize\s*=\s*yes/daemonize = no/g' /usr/local/etc/php-fpm.d/www.conf

#RUN echo "http://nl.alpinelinux.org/alpine/latest-stable/main" > /etc/apk/repositories \
#&& echo "http://nl.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories \
#&& echo "http://nl.alpinelinux.org/alpine/edge/community/" >> /etc/apk/repositories \
#&& echo "nameserver 8.8.8.8" >> /etc/resolv.conf 

#&& rm -rf /tmp/* 
RUN apk update && \

#安装redis,xdebug
#RUN pecl install redis-3.1.2 \
#&& pecl install xdebug-2.6.0 \
#&& docker-php-ext-enable redis xdebug
 set -xe \
    && apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
    && pecl install -o -f redis  \
    && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
    && rm -rf /usr/share/php \
    && rm -rf /tmp/* \
    && apk del  .phpize-deps && \
#安装GD库,MYSQL扩展
apk add --update libpng libpng-dev && \
docker-php-ext-install gd pdo_mysql mysqli

RUN docker-php-ext-install zip && bcmath
