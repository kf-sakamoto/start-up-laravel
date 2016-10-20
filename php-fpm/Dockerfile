FROM php:7-fpm

MAINTAINER Fukuyama Nobukazu <fukuyama@kf-works.co.jp>

RUN apt-get update && apt-get install -y \
   libpq-dev \
   libmemcached-dev \
   curl \
   libpng12-dev \
   libfreetype6-dev \
   libssl-dev \
   libmcrypt-dev \
   --no-install-recommends \
   && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install mcrypt

RUN docker-php-ext-configure gd \
   --enable-gd-native-ttf \
   --with-freetype-dir=/usr/include/freetype2

RUN docker-php-ext-install \
   pdo_mysql \
   gd

RUN apt-get update

RUN apt-get install -y default-jdk

WORKDIR /var/www/laravel

EXPOSE 9000

CMD ["php-fpm"]
