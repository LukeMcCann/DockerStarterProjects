FROM php:7.2-fpm-alpine

RUN apk update && apk add curl && \
  curl -sS https://getcomposer.org/installer | php \
    && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/html

COPY composer.json composer.lock ./
RUN composer install --no-scripts --no-autoloader

COPY . .
RUN chmod +x artisan

RUN composer dump-autoload --optimize && composer run-script post-install-cmd

LABEL maintainer="Nick Janetakis <nick.janetakis@gmail.com>"

CMD php artisan serve --host 0.0.0.0 --port 5000
