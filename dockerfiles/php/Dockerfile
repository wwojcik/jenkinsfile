FROM php:fpm-alpine
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data --enable-redis-igbinary
ENV TIMEZONE=Europe/Warsaw
RUN apk add --update postgresql-dev freetype-dev libjpeg-turbo-dev libmcrypt-dev libpng-dev
RUN docker-php-ext-install bcmath iconv mcrypt intl opcache zip ctype json mbstring xml pdo_pgsql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/pear \
    && rm -rf /usr/src/php
COPY config/php.ini /usr/local/etc/php/
CMD ["php-fpm"]
