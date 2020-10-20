# Docker image for ethicaljobs/php-api: 
Foundation image for all PHP APIs that EthicalJobs operates.

Dockerhub: https://hub.docker.com/repository/docker/ethicaljobs/php-api

## Supported tags and respective Dockerfile links
- [7.4](https://github.com/ethical-jobs/docker-php-api/tree/master/7.4/)

## Features
 - FastCGI Process Manager (php-fpm)
 - base from official `php-alpine`
 - PHP extensions `mysqli`, `pdo_mysql`, `opcache`, `pcntl`, `bcmath`, `exif`, `gd`
 - `composer` binary with [prestissimo](https://github.com/hirak/prestissimo) installed

## Xdebug
xdebug module is present in the image, but is not loaded as a PHP extension in the default runtime.

You can lazily load the module in by using

```bash
php -d zend_extension=xdebug ... 
```

or providing your own `php.ini` with the extension enabled
