# WordPress Docker Setup for Development

- WordPress 5.7.1
- WP CLI 2.4.0
- PHP 8 (JIT-enabled)
- Xdebug 3
- MySQL 8
- phpMyAdmin
- MailHog

### Start Services

```
docker-compose up -d
```

| Service    | Default URL
|:-----------|:---------------------|
| WordPress  | [http://localhost:8000/](http://localhost:8000/) 
| phpMyAdmin | [http://localhost:8001/](http://localhost:8001/) 
| MailHog    | [http://localhost:8025/](http://localhost:8025/)

### Mounted WP folder
Docker expects to find WordPress in a `src/` folder. If it doesn't exist, it creates it and installs WordPress inside. Visit [http://127.0.0.1:8000](http://127.0.0.1:8000) to finish the database installation.

### Helper executables

Use the [`./wp`](wp) to run WP CLI commands.

Use the [`./composer`](composer) to run composer commands in the WordPress Container.

### Logs

Monitor the PHP logs from the WordPress container with:

```
docker logs -f $(docker-compose ps -q wp) >/dev/null
```

### Debugging

Xdebug 3 is pre-configured for remote debugging with the IDE key `PHPSTORM`. See [php.ini](dockerenv/php.ini).