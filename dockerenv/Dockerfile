FROM composer:2 as composer

FROM wordpress:5.7.2-php8.0

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN apt-get update \
    && apt-get install -q -y libmcrypt-dev default-mysql-client msmtp mailutils less \
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug \
	&& curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x /usr/local/bin/wp \

