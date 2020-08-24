FROM php:7.4-cli-alpine

# Install dependencies
RUN apk add --no-cache \
    build-base  \
    gcc  \
    wget  \
    git \
    zlib-dev \
    bash \
    libzip-dev \
    zip \
    unzip \
    curl \
    libpng-dev \
    libxml2-dev

# Install extensions
RUN docker-php-ext-install -j$(nproc) pdo_mysql zip exif bcmath pcntl gd

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require --update-no-dev --prefer-dist \
        psy/psysh:@stable \
        nesbot/carbon \
        laravel/installer \
        laravel-zero/installer \
        icanhazstring/composer-unused \
    && composer clear-cache

COPY .bashrc /root/.bashrc

WORKDIR /app