FROM php:7.4-fpm-alpine AS php

LABEL maintainer="Ethical Jobs <development@ethicaljobs.com.au>"

FROM php AS system_environment

RUN apk add --no-cache oniguruma-dev $PHPIZE_DEPS \
    && pecl install xdebug && pecl clear-cache \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && echo $NPROC \
    && docker-php-ext-install -j${NPROC} \
        mysqli \
        pdo_mysql \
        opcache \
        pcntl \
        bcmath \
        exif \
        mbstring \
    && docker-php-source delete \
    && apk del --no-network oniguruma-dev $PHPIZE_DEPS --purge

FROM php AS composer

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
    && composer global require --prefer-dist --no-suggest --no-progress "hirak/prestissimo" \
    && composer global clear-cache
