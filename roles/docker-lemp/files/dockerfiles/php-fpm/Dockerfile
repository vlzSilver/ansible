FROM php:8.4-rc-fpm-alpine3.20

COPY ./files/example-site /var/www/html/

COPY ./files/php-fpm-healthcheck /usr/local/bin/

RUN docker-php-ext-install -j$(nproc) pdo_mysql

RUN apk add --no-cache fcgi bash && chmod +x /usr/local/bin/php-fpm-healthcheck

RUN set -xe && echo "pm.status_path = /status" >> /usr/local/etc/php-fpm.d/zz-docker.conf

