FROM php:7.1.2-fpm

# Install dependencies
RUN apt-get update && apt-get install -y wget unzip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libbz2-dev \
        libssl-dev
RUN docker-php-ext-install -j$(nproc)  mcrypt pdo_mysql
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install \
        bcmath \
        bz2 \
        exif \
        ftp \
        gd \
        gettext \
        mbstring \
        opcache \
        shmop \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        zip \
        iconv

# Download the latest Craft source
RUN wget 'http://download.buildwithcraft.com/craft/2.6/2.6.2967/Craft-2.6.2967.zip' -O "/craft-source.zip"

# Unzip it into the correct location
RUN unzip -qqo /craft-source.zip -d /var/www/html

COPY ./src/public /var/www/html/public
COPY ./src/config /var/www/html/craft/config
COPY ./src/templates /var/www/html/craft/templates
COPY ./src/plugins /var/www/html/craft/plugins

RUN chmod -R 777 /var/www/html/craft/storage
RUN chmod -R 777 /var/www/html/craft/app
RUN chmod -R 777 /var/www/html/craft/config

