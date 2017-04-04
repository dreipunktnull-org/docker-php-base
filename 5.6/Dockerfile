FROM php:5.6

RUN apt-get update -yqq && \
    apt-get install git wget unzip libxslt-dev libzip-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev -yqq && \
    docker-php-ext-install -j$(nproc) xsl zip iconv mcrypt pdo_mysql exif pcntl && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd
