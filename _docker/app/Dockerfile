FROM php:8.0-fpm

RUN apt-get update && apt-get install -y \
        curl \
        wget \
        git \
        sendmail \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libonig-dev \
        libzip-dev \
        && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
	    && docker-php-ext-configure gd --with-freetype --with-jpeg \
        && docker-php-ext-install -j$(nproc) gd

COPY ./_docker/app/php.ini /usr/local/etc/php/conf.d/php.ini

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

WORKDIR /var/www/html