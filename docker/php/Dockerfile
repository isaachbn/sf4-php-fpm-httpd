FROM php:7.2.10-fpm

MAINTAINER Isaac Henrique <isaachbnn@gmail.com>

RUN apt-get update \
    && apt-get install -y --no-install-recommends libpq-dev vim curl debconf subversion git apt-transport-https apt-utils \
    build-essential locales acl mailutils wget zip unzip \
    gnupg gnupg1 gnupg2 \
    zlib1g-dev

RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
  && docker-php-ext-install pdo_pgsql pgsql zip

COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm-pool.conf 	/usr/local/etc/php/pool.d/www.conf

RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
	mv composer.phar /usr/local/bin/composer

# Set timezone
RUN ln -snf /usr/share/zoneinfo/America/Recife /etc/localtime && echo America/Recife > /etc/timezone \
    && printf '[PHP]\ndate.timezone = "%s"\n', America/Recife > /usr/local/etc/php/conf.d/tzone.ini \
    && "date"

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "pt_BR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

#FROM php:7.2-fpm-alpine
#
#MAINTAINER Isaac Henrique <isaachbnn@gmail.com>
#
#RUN set -ex \
#  	&& apk update \
#    && apk add --no-cache git zip curl openssh-client icu libpng freetype libjpeg-turbo postgresql-dev libffi-dev libsodium \
#    && apk add --no-cache --virtual build-dependencies icu-dev libxml2-dev freetype-dev libpng-dev libjpeg-turbo-dev g++ make autoconf libsodium-dev \
#    && docker-php-source extract \
#    && pecl install xdebug redis libsodium \
#    && docker-php-ext-enable xdebug redis sodium \
#    && docker-php-source delete \
#    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
#    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#    && docker-php-ext-install -j$(nproc) pdo pgsql pdo_mysql pdo_pgsql intl zip gd mbstring \
#    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
#    && apk del build-dependencies \
#    && rm -rf /tmp/*
#
#USER www-data