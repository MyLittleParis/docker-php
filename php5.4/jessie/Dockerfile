FROM alterway/php:5.4-fpm

# patch source list for jessie
RUN echo "deb http://deb.debian.org/debian/ jessie main contrib non-free \n\
          deb-src http://deb.debian.org/debian/ jessie main contrib non-free \n\
          deb http://security.debian.org/ jessie/updates main contrib non-free \n\
          deb-src http://security.debian.org/ jessie/updates main contrib non-free" > /etc/apt/sources.list

RUN docker-php-ext-install soap \
    && echo 'memory_limit = -1' >> $PHP_INI_DIR/conf.d/00-default.ini

RUN apt-get update \
    && apt-get install -y npm \
    && ln -s /usr/bin/nodejs /usr/bin/node

RUN npm install -g less \
    && npm install -g bower

RUN apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

CMD ["php-fpm"]
