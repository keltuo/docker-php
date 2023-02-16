FROM php:8.1-cli
ENV TZ=Europe/Prague

RUN apt-get update -yqq
RUN apt-get install git -yqq
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN rm /etc/localtime \
    && ln -s /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "$TZ" > /etc/timezone
RUN echo "date.timezone = $TZ" >> /usr/local/etc/php/php.ini
RUN apt-get clean \
        && apt-get autoremove -y \
        && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/

ENTRYPOINT ["docker-php-entrypoint"]
