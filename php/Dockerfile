FROM php:fpm

# For composer
RUN apt-get update \
    && apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && mv composer.phar /usr/local/bin/composer

# Set composer environment
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Install laravel installer
RUN composer global require "laravel/installer"

# PHP's DB setting
RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql pdo_pgsql

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs

WORKDIR /src
