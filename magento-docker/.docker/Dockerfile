ARG VERSION=7.1.27
FROM php:${VERSION}-apache

# php extensions install
RUN apt-get update
RUN apt-get install -y zlib1g-dev libpq-dev libicu-dev libpng-dev \
      libjpeg62-turbo-dev libfreetype6-dev libxml2-dev libxslt-dev wget zip unzip git

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install zip intl gd bcmath soap xsl mysqli pdo_mysql mbstring \
    && cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

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

# copy magento credentials
COPY composer/auth.json /root/.composer/

# workspace
WORKDIR /var/www/html
