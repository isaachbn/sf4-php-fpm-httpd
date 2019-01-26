FROM php:7.2-fpm-alpine

MAINTAINER Isaac Henrique <isaachbnn@gmail.com>

RUN set -ex \
  	&& apk update \
    && apk add --no-cache git zip curl openssh-client icu libpng freetype libjpeg-turbo postgresql-dev libffi-dev libsodium \
    && apk add --no-cache --virtual build-dependencies icu-dev libxml2-dev freetype-dev libpng-dev libjpeg-turbo-dev g++ make autoconf libsodium-dev \
    && docker-php-source extract \
    && pecl install xdebug redis libsodium \
    && docker-php-ext-enable xdebug redis sodium \
    && docker-php-source delete \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) pdo pgsql pdo_mysql pdo_pgsql intl zip gd mbstring \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apk del build-dependencies \
    && rm -rf /tmp/*

COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm-pool.conf 	/usr/local/etc/php/pool.d/www.conf
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug-dev.ini
USER www-data
CMD ["php-fpm"]