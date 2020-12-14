FROM php:7.4-fpm-alpine

#
# Copy project
#
WORKDIR  /var/www
COPY    ./project .

#
# Install some useful stuff
#
RUN apk update && apk add --no-cache \
    nano \
    wget \
    autoconf \
    build-base \
    curl \
    dpkg-dev \
    gcc \
    git \
    grep \
    icu-dev \
    libc-dev \
    libgsasl-dev \
    libmcrypt-dev \
    libxml2-dev \
    libzip-dev \
    oniguruma-dev \
    zlib-dev \
    make \
    openssl-dev

#
# Install APCU
#
RUN pecl install apcu && docker-php-ext-enable apcu

#
# Install some PHP docker extensions
#
RUN docker-php-ext-install \
    opcache \
    mbstring \
    bcmath \
    pcntl \
    iconv \
    intl \
    pdo \
    intl \
    pdo_mysql \
    zip

#
# Composer
#
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN composer install

#
# Copy config
#
COPY ./docker/php/config.ini $PHP_INI_DIR/conf.d/config.ini
#COPY ./docker/php/www.conf   $PHP_INI_DIR/conf.d/www.conf

#
# Cleanup
#
RUN apk del --no-cache wget autoconf gcc libc-dev make

#
# Finish
#
EXPOSE 9000
CMD ["php-fpm"]

