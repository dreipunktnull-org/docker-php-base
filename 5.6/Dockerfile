FROM php:5.6

RUN apt-get update -yqq && \
    apt-get install apt-transport-https git wget unzip libxslt-dev libzip-dev libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev -yqq && \
    yes | pecl install xdebug && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini && \
    docker-php-ext-install -j$(nproc) xsl zip iconv mcrypt pdo_mysql exif pcntl && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    docker-php-ext-enable xdebug && \
    rm -rf /var/lib/apt/lists/*

# Grab a composer
RUN mkdir -p /opt/composer \
    && mkdir -p /opt/bin \
    && cd /opt/composer \
    && php -r "copy('https://composer.github.io/installer.sig', 'composer-installer.sig');" \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('./composer-installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && chmod +x /opt/composer/composer.phar \
    && ln -s /opt/composer/composer.phar /opt/bin/composer \
    && cd /

# Expand path to opt
ENV PATH /opt/bin:$PATH
