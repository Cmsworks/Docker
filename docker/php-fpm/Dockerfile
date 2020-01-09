FROM php:7.2-fpm

RUN apt-get update && apt-get install -y wget git unzip \
    && pecl install xdebug-2.9.0 \
    && docker-php-ext-enable xdebug

ADD php.ini /usr/local/etc/php/php.ini

RUN echo "$(curl -sS https://composer.github.io/installer.sig) -" > composer-setup.php.sig \
    && curl -sS https://getcomposer.org/installer | tee composer-setup.php | sha384sum -c composer-setup.php.sig \
    && php composer-setup.php && rm composer-setup.php* \
    && chmod +x composer.phar && mv composer.phar /usr/bin/composer

WORKDIR /var/www
EXPOSE 9001
