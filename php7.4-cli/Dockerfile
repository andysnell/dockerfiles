FROM php:7.4-cli

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    zlib1g-dev \
    libzip-dev \
    zip \
    unzip \
    git \
    curl \
    libpng-dev \
    libxml2-dev

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install -j$(nproc) pdo_mysql zip exif bcmath pcntl gd

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require \
    psy/psysh:@stable \
    hirak/prestissimo \
    nesbot/carbon \
    laravel/installer \
    laravel-zero/installer \
    icanhazstring/composer-unused

COPY .bashrc /root/.bashrc

WORKDIR /app