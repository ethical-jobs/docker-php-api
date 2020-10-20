FROM php:7.4-fpm-alpine AS php

LABEL maintainer="Ethical Jobs <development@ethicaljobs.com.au>"

# Remove html directory php base image creates
RUN rm -rf /var/www/html
WORKDIR /var/www

RUN apk add --no-cache --virtual .ej-deps oniguruma-dev freetype-dev libzip-dev \
        libjpeg-turbo-dev libpng-dev zlib $PHPIZE_DEPS \
    && pecl channel-update pecl.php.net && pecl install xdebug && pecl clear-cache \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j${NPROC} \
        mysqli \
        pdo_mysql \
        opcache \
        pcntl \
        bcmath \
        exif \
        gd \
    && docker-php-source delete \
    && apk del --no-network .ej-deps \
    && apk add --no-cache freetype libjpeg-turbo libpng

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && composer global require --prefer-dist --no-suggest --no-progress "hirak/prestissimo" \
    && composer global clear-cache
