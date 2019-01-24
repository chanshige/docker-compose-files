FROM php:7.3.1-apache

# php extensions install
RUN apt-get update
RUN apt-get install -y libicu-dev libpng-dev \
      && docker-php-ext-install intl gd

# composer install
RUN curl -sS https://getcomposer.org/installer | php \
      && mv composer.phar /usr/local/bin/composer

# composer setup
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# install xdebug
RUN pecl install xdebug-beta \
      && docker-php-ext-enable xdebug

# apache:mod_rewrite
RUN a2enmod rewrite

WORKDIR /var/www/html
