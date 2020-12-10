# Docker image for ethicaljobs/php-api: 
Base image for the EthicalJobs PHP runtime 

[Dockerhub - ethicaljobs/php-api](https://hub.docker.com/repository/docker/ethicaljobs/php-api)

```
docker pull ethicaljobs/php-api:<tag>
```

## Supported tags and respective Dockerfile links
- [7.4](https://github.com/ethical-jobs/docker-php-api/tree/master/7.4/)
  - PHP 7.4.3
  - composer v1.10.5
  - no PHP GD module
  - xdebug v2.9.4
- [7.4-gd](https://github.com/ethical-jobs/docker-php-api/tree/master/7.4/)
  - PHP 7.4.3
  - composer v1.10.13
  - xdebug v2.9.8
- [8.0](https://github.com/ethical-jobs/docker-php-api/tree/master/8.0/)
  - PHP 8.0.0
  - Composer v2.0.7
  - xdebug v3.0.1
  - working directory changed to `/var/www` (formerly `/var/www/html`)

## Features
 - FastCGI Process Manager (php-fpm)
 - Extends official `php-alpine`
 - PHP extensions `mysqli`, `pdo_mysql`, `opcache`, `pcntl`, `bcmath`, `exif`, `gd`

## User
As per official php-fpm image, the image runs as root by default. See their README for further details running with abitrary users.

FPM workers will run as user `www-data`

## Xdebug
xdebug module is present in the image, but is not loaded as a PHP extension for the default runtime.

You can lazily load the module in by using

```bash
php -d zend_extension=xdebug ... 
```

or providing your own `php.ini` with the extension enabled
