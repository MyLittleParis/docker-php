FROM alterway/php:5.4-fpm

RUN apt-get update \
    && apt-get install -y npm \
    && ln -s /usr/bin/nodejs /usr/bin/node

RUN npm install -g less \
    && npm install -g bower

RUN apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

CMD ["php-fpm"]