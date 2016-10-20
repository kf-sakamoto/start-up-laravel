FROM debian:jessie

MAINTAINER Fukuyama Nobukazu <fukuyama@kf-works.co.jp>

RUN apt-get update && \
    apt-get install -y --force-yes wget

RUN echo deb http://packages.dotdeb.org jessie all >> /etc/apt/sources.list && \
    echo deb-src http://packages.dotdeb.org jessie all >> /etc/apt/sources.list

RUN wget https://www.dotdeb.org/dotdeb.gpg && \
    apt-key add dotdeb.gpg

RUN apt-get update && \
    apt-get install -y --force-yes \
        php7.0-cli \
        php7.0-common \
        php7.0-curl \
        php7.0-json \
        php7.0-xml \
        php7.0-mbstring \
        php7.0-mcrypt \
        php7.0-mysql \
        php7.0-pgsql \
        php7.0-sqlite \
        php7.0-sqlite3 \
        php7.0-zip \
        php7.0-memcached \
        php7.0-gd \
        php7.0-xdebug \
        php-dev \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        sqlite3 \
        libsqlite3-dev \
        git \
        curl \
        vim \
        nano

RUN apt-get clean && \
    rm dotdeb.gpg

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/laravel
