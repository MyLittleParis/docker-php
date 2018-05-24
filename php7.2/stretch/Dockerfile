ARG php_version=7.2
ARG os_version=stretch
FROM php:${php_version}-fpm-${os_version}

# install extension dependencies and install dep
RUN apt-get update \
    && apt-get install -y \
      zlib1g-dev libicu-dev g++ libpng.dev libcurl4-gnutls-dev librtmp-dev git \
      libmcrypt-dev libxml++2.6-dev libc-client-dev libkrb5-dev \
      curl software-properties-common gnupg \
    && ln -s /usr/bin/nodejs /usr/bin/node \
    && docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
    && docker-php-ext-install intl gd curl json mbstring mcrypt opcache pdo xml zip pdo_mysql imap \
    && echo 'date.timezone = "Europe/Paris"' >> /usr/local/etc/php/php.ini

# Install composer and set alias for easier use
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
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
