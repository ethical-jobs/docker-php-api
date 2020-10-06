# Docker image for ethicaljobs/php-api: 
Foundation image for all PHP APIs that EthicalJobs operates.

Dockerhub: https://hub.docker.com/repository/docker/ethicaljobs/php-api

## Supported tags and respective Dockerfile links
- [7.4](https://github.com/ethical-jobs/docker-php-api/tree/master/7.4/)
- [7.4-gd](https://github.com/ethical-jobs/docker-php-api/tree/master/7.4-gd/) Includes GD module + required system libs

## Information

All images contain the following features:
 - Base off the official `php-alpine` variant
 - composer binary with prestissimo

## XDebug
The XDebug module is included in all base images, but is not loaded by default as an extension.
When using the image for remote debugging, or local development be sure to lazily load in the module, or adjust your `php.ini` to include the extension.

```bash
php -d zend_extension=xdebug ... 
```
