FROM php:8.0.0-fpm-alpine AS xdebug

RUN wget https://xdebug.org/files/xdebug-3.0.1.tgz -q -S -P /tmp \
    && apk add --no-cache --virtual .deps $PHPIZE_DEPS \
    && pear install /tmp/xdebug-3.0.1.tgz \
    && rm /tmp/xdebug-3.0.1.tgz \
    && apk del --no-network .deps

FROM php:8.0.0-fpm-alpine AS php

LABEL maintainer="Ethical Jobs <development@ethicaljobs.com.au>"

COPY --from=xdebug /usr/local/lib/php/extensions/no-debug-non-zts-20200930/xdebug.so /usr/local/lib/php/extensions/no-debug-non-zts-20200930/
COPY --from=composer:2.0.7 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

RUN apk add --no-cache --virtual .deps zlib-dev libpng-dev freetype-dev libjpeg-turbo-dev $PHPIZE_DEPS \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && NPROC=$(getconf _NPROCESSORS_ONLN) \
    && docker-php-ext-install -j${NPROC} \
        pdo_mysql \
        mysqli \
        opcache \
        pcntl \
        bcmath \
        exif \
        gd \
    && apk del --no-network .deps \
    && apk add --no-cache freetype libjpeg-turbo libpng \
    && rm -rf /usr/src/* \
    && rm -rf /var/www/html \
    && chown www-data:www-data /var/www \
    && chmod 755 /var/www

ENV COMPOSER_ALLOW_SUPERUSER=1

