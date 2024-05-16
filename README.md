# Setup Wordpress for local development with Docker Compose

This repository contains a Docker Compose setup for running WordPress with Nginx as a web server and PHP-FPM.

## Requirements

- Docker
- Docker Compose

## Getting Started

1. Clone this repository:

   ``` console 
   git clone https://github.com/abiandreb/wordpress-local-docker
   ```

2. Navigate to the cloned repository:
   ``` console 
   cd wordpress-local-docker
   ```
3. Start the containers:
   ``` console 
   docker-compose up -d --build
   ```
4. Access WordPress in your web browser at http://localhost.

## Configuration

### Nginx Configuration

The Nginx configuration is defined in the `nginx.conf` file.

```
upstream php {
    server unix:/tmp/php-cgi.socket;
    server php:9000;
}

server {
    listen 80;
    server_name localhost;

    root /var/www/html;

    location / {
        try_files $uri /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi.conf;
        fastcgi_intercept_errors on;
        fastcgi_pass php;
    }
}
```
### Dockerfile for PHP

The Dockerfile for PHP is defined as `php/Dockerfile`.

```docker
FROM php:7.4-fpm-alpine

RUN docker-php-ext-install mysqli pdo pdo_mysql  && docker-php-ext-enable pdo_mysql
```
## License

This project is licensed under the MIT License.
