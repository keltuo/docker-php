FROM php:8.1-cli
ENV TZ=Europe/Prague

RUN apt-get update -yqq
RUN apt-get install git -yqq
RUN pecl install xdebug && docker-php-ext-enable xdebug 
RUN apt-get install -y libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl
RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "$TZ" > /etc/timezone
RUN echo "date.timezone = $TZ" >> /usr/local/etc/php/php.ini

WORKDIR /var/www/

ENTRYPOINT ["docker-php-entrypoint"]

