FROM php:7.2-fpm

RUN apt-get update && apt-get install -y wget git unzip \
    && docker-php-ext-install pdo pdo_mysql \
    && pecl install xdebug-2.9.0 \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install opcache

ADD php.ini /usr/local/etc/php/php.ini

# install composer
RUN echo "$(curl -sS https://composer.github.io/installer.sig) -" > composer-setup.php.sig \
    && curl -sS https://getcomposer.org/installer | tee composer-setup.php | sha384sum -c composer-setup.php.sig \
    && php composer-setup.php && rm composer-setup.php* \
    && chmod +x composer.phar && mv composer.phar /usr/bin/composer

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime
RUN "date"

WORKDIR /var/www
EXPOSE 9001
