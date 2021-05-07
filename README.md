# WordPress Docker Setup for Development

- WordPress 5.7.1
- WP CLI 2.4.0
- PHP 8
- MySQL 8
- phpMyAdmin
- MailHog

### Start Services

```
docker-compose up -d
```

| Service    | Default URL
|:-----------|:---------------------|
| WordPress  | http://localhost:8000/ 
| phpMyAdmin | http://localhost:8001/ 
| MailHog    | http://localhost:8025/


### Helper executables

Use the `./wp` to run WP CLI commands.

Use the `./composer` to run composer commands in the WordPress Container.
