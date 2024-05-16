FROM php:7.4-fpm-alpine

RUN docker-php-ext-install mysqli pdo pdo_mysql bcmath exif && docker-php-ext-enable pdo_mysql bcmath exif

RUN set -ex \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable imagick \
    && apk add --no-cache --virtual .imagick-runtime-deps imagemagick \
    && apk del .phpize-deps

RUN apk add --no-cache libpng libpng-dev && docker-php-ext-install gd && apk del libpng-dev

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
