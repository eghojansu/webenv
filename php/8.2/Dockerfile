FROM php:8.2-cli-alpine

# Install system dependencies
RUN apk update && apk add --no-cache \
    libzip-dev \
    libpng-dev \
    icu-dev

# Install PHP extensions
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    zip \
    gd \
    intl

# Install Composer
COPY --from=composer:2.5.7 /usr/bin/composer /usr/local/bin/composer

WORKDIR /home/www-data