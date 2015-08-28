FROM php:7.0-cli

ADD php/php.ini /usr/local/etc/php/php.ini

# Add 10gen official apt source to the sources list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/debian wheezy/mongodb-org/3.0 main" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list
# Install MongoDB and dependencies for intl and zip extensions
RUN apt-get update && apt-get upgrade -y && apt-get install -y mongodb-org libicu-dev g++ sudo zlib1g-dev git libssl-dev

RUN echo "y\ny" | pecl install apcu-beta
ADD php/apcu.ini /usr/local/etc/php/conf.d/apcu.ini
RUN docker-php-ext-install bcmath mbstring opcache intl pcntl zip
ADD php/opcache.ini /usr/local/etc/php/conf.d/ext-opcache.ini
RUN pecl install mongo-1.6.10
ADD php/mongo.ini /usr/local/etc/php/conf.d/mongo.ini

# install composer
RUN cd /usr/local/bin/ && curl -sS https://getcomposer.org/installer | php

# Compact docker
RUN apt-get clean -y  && rm -rf /tmp/pear/*

ADD sudo/sudoers /etc/sudoers

CMD /usr/bin/mongod --smallfiles --dbpath /var/lib/mongodb/ --replSet rs1 --logpath /var/log/mongodb/mongodb.log --fork && \
    /usr/bin/mongo --eval 'rs.initiate();' && \
    /data/bin/phpunit -c /data/app/
