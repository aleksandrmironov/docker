FROM ubuntu:14.04

MAINTAINER Aleksandr Mironov <amironov@level5ops.com>

#add ondrej repo and install php pkgs
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y --force-yes \
    php7.1 \
    php-pear \
    php7.1-cgi \
    php7.1-cli \
    php7.1-common \
    php7.1-curl \
    php7.1-dev \
    php7.1-imap \
    php7.1-mcrypt \
    php7.1-mysql \
    php7.1-gd \
    php-redis

# install pecl ext
RUN add-apt-repository ppa:pinepain/libv8-5.2 && \
    apt-get update && \
    apt-get install -y --force-yes libv8-5.2-dev && \
    printf "\n" | pecl install v8js && \
    rm -r /var/lib/apt/lists/*

COPY v8js.ini /etc/php/7.1/mods-available/v8js.ini

COPY php.ini /etc/php/7.1/cli/v8js.ini

RUN phpenmod v8js

ENTRYPOINT ["php", "-f"]