# docker-php

image: keltuo/php:8-cli

image: keltuo/php:7.4-cli

TAGS[https://hub.docker.com/r/keltuo/php/tags]

GITHUB[https://github.com/keltuo/docker-php]

docker-compose.yml

```
version: "3"
services:
  php:
    container_name: php-sm
    image: keltuo/php:8-cli
    volumes:
      - ./:/var/www/
    command: bash -c "php /var/www/vendor/phpunit/phpunit/phpunit --configuration /var/www/phpunit.xml"
  composer:
    container_name: composer-sm
    image: composer
    volumes:
      - ./:/app
    command: bash -c "composer install --optimize-autoloader --prefer-dist --no-progress"
```
