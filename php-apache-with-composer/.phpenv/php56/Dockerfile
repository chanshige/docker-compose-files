FROM php:5.6.40-apache

# php extensions install
RUN apt-get update
RUN apt-get install -y zlib1g-dev libpq-dev libicu-dev libpng-dev wget zip unzip \
      && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
      && docker-php-ext-install intl gd mysqli pdo_mysql pdo_pgsql pgsql mbstring

# composer install
RUN curl -sS https://getcomposer.org/installer | php \
      && mv composer.phar /usr/local/bin/composer

# composer setup
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# install xdebug
RUN pecl install xdebug \
      && docker-php-ext-enable xdebug

# apache:mod_rewrite
RUN a2enmod rewrite

WORKDIR /var/www/html
