FROM php:5.5-cli

ADD php/php.ini /usr/local/etc/php/php.ini
RUN pecl install mongo
ADD php/mongo.ini /usr/local/etc/php/conf.d/mongo.ini

# Add 10gen official apt source to the sources list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list
# Install MongoDB
RUN apt-get update && apt-get upgrade -y && apt-get install -y mongodb-org

RUN echo "y\ny" | pecl install apcu-beta
ADD php/apcu.ini /usr/local/etc/php/conf.d/apcu.ini

# Compact docker
RUN apt-get clean -y  && rm -rf /tmp/pear/*

CMD /usr/bin/mongod --smallfiles --dbpath /var/lib/mongodb/ --replSet rs1 --logpath /var/log/mongodb/mongodb.log --fork && \
    /usr/bin/mongo --eval 'rs.initiate();' && \
    /data/bin/phpunit -c /data/app/
