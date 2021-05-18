# WordPress Docker Setup for Development

This setup is for local development only. **DO NOT** use in production.

- [WordPress 5.7.2](https://wordpress.org)
- [WP CLI 2.4.0](https://wp-cli.org/)
- [PHP 8 (JIT-enabled)](https://www.php.net/releases/8.0/en.php)
- [Composer 2](https://getcomposer.org)
- [Xdebug 3](https://xdebug.org)
- Apache
- MariaDB 10.6
- [phpMyAdmin 5.1](https://www.phpmyadmin.net)
- [MailHog](https://github.com/mailhog/MailHog)

### Start Services

```
docker-compose up -d
```

| Service    | Default URL
|:-----------|:---------------------|
| WordPress  | [http://localhost:8000/](http://localhost:8000/) 
| phpMyAdmin | [http://localhost:8001/](http://localhost:8001/) 
| MailHog    | [http://localhost:8025/](http://localhost:8025/)
| MariaDB    | `localhost:3306`

## Mounted WP folder
Docker expects to find WordPress in a `web/` folder. If it doesn't exist, it creates it and installs WordPress inside. Visit [http://127.0.0.1:8000](http://127.0.0.1:8000) to finish the database installation.

## Helper executables

Use the [`./wp`](wp) to run WP CLI commands in the WordPress container.

Use the [`./composer`](composer) to run composer commands in the WordPress Container.

## Database

phpMyAdmin is running on [http://127.0.0.1:8001](http://127.0.0.1:8001) and also port `3306` gets automatically bound to your host so you can connect with an SQL client.

## Logs

Monitor the PHP logs from the WordPress container with:

```
docker logs -f $(docker-compose ps -q wp) >/dev/null
```

## Debugging

Xdebug 3 is pre-configured for remote debugging with the IDE key `PHPSTORM`. See [php.ini](dockerenv/php.ini).

## Multisite

For multisite support in sub-directory mode, add this to your `.htaccess`:

```
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^wp-admin$ wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^(wp-(content|admin|includes).*) $1 [L]
RewriteRule ^(.*\.php)$ $1 [L]
RewriteRule . index.php [L]
```

And this to your `wp-config.php`:

```php
define('WP_ALLOW_MULTISITE', true);
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', '127.0.0.1:8000');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```
