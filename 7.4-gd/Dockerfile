FROM php:7.4-fpm-alpine AS php

LABEL maintainer="Ethical Jobs <development@ethicaljobs.com.au>"

RUN apk add --no-cache oniguruma-dev freetype-dev libzip-dev \
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
    && apk del --no-network oniguruma-dev freetype-dev libzip-dev \
        libjpeg-turbo-dev libpng-dev zlib $PHPIZE_DEPS --purge \
    && apk add --no-cache freetype libjpeg-turbo libpng

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && composer global require --prefer-dist --no-suggest --no-progress "hirak/prestissimo" \
    && composer global clear-cache

RUN set -ex && \
    rm -f /usr/libexec/gcc/x86_64-alpine-linux-musl/6.4.0/cc1obj && \
    rm -f /usr/libexec/gcc/x86_64-alpine-linux-musl/6.4.0/lto1 && \
    rm -f /usr/libexec/gcc/x86_64-alpine-linux-musl/6.4.0/lto-wrapper && \
    rm -f /usr/bin/x86_64-alpine-linux-musl-gcj
