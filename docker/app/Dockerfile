FROM php:8.4-fpm

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

RUN apt-get update \
    && apt-get install -y \
        libxslt1-dev \
        librabbitmq-dev \
        libssl-dev \
        default-mysql-client \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
    && docker-php-ext-install pdo_mysql opcache xsl \
    && install-php-extensions xdebug zip amqp gd intl

RUN groupadd -g 1000 app && useradd -u 1000 -ms /bin/bash -g app app

ENV PHP_IDE_CONFIG 'serverName=sandbox_database'
COPY ./conf.d /usr/local/etc/php/conf.d

WORKDIR /app

USER app
