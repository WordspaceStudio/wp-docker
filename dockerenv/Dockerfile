FROM composer:2 as composer

FROM wordpress:5.7.1-php8.0

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN apt-get update \
    && apt-get install -q -y libmcrypt-dev default-mysql-client msmtp mailutils \
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug \

