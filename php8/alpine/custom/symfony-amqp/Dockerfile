FROM php:8.0.7-fpm-alpine3.12

COPY php_custom.ini /usr/local/etc/php/conf.d/

RUN apk add libxml2-dev php-soap \
  && docker-php-ext-install soap \
  && apk update && apk add --no-cache git openssh zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


RUN apk --update add libxml2-dev php-soap git supervisor \
  && docker-php-ext-install soap pdo pdo_mysql
RUN apk --update add gcc make g++ zlib-dev && apk add rabbitmq-c rabbitmq-c-dev autoconf
RUN docker-php-source extract \
    && mkdir /usr/src/php/ext/amqp \
    && curl -L https://github.com/php-amqp/php-amqp/archive/master.tar.gz | tar -xzC /usr/src/php/ext/amqp --strip-components=1 \
    && docker-php-ext-install amqp
RUN docker-php-ext-install sockets && docker-php-ext-enable amqp

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY ./ /var/www/html

RUN chown www-data:www-data -R /var/www/html

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

WORKDIR /var/www/html

