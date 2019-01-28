ARG php_version=5.6
ARG os_version=stretch
FROM php:${php_version}-fpm-${os_version}

# install extension dependencies and install dep
RUN apt-get update \
    && apt-get install -y \
      zlib1g-dev libicu-dev g++ libpng.dev libcurl4-gnutls-dev libmagickwand-dev librtmp-dev git \
      libmcrypt-dev libxml++2.6-dev libc-client-dev libkrb5-dev \
      curl software-properties-common gnupg \
    && ln -s /usr/bin/nodejs /usr/bin/node \
    && pecl install imagick apcu-4.0.11 \
    && docker-php-ext-enable imagick apcu \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-configure gd --with-gd --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ --with-freetype-dir=/usr/include/ \
    && docker-php-ext-install intl gd curl json mbstring mcrypt opcache pdo xml zip pdo_mysql imap bcmath \
    && echo 'date.timezone = "Europe/Paris"' >> /usr/local/etc/php/php.ini \
    && echo 'memory_limit = -1' >> /usr/local/etc/php/php.ini

# Install composer and set alias for easier use
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer \
    && php -r "unlink('composer-setup.php');"

# Install node and npm
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - \
    && apt-get install nodejs \
    && npm install -g less bower

# Remove useless packages
RUN apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Set start command for entrypoint
CMD ["php-fpm"]
