FROM php:8.1-cli
ENV TZ=Europe/Prague

RUN apt-get update -yqq
RUN apt-get install git curl zip unzip -yqq
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "$TZ" > /etc/timezone
RUN echo "date.timezone = $TZ" >> /usr/local/etc/php/php.ini

RUN apt-get clean
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

WORKDIR /var/www/

ENTRYPOINT ["docker-php-entrypoint"]
