FROM node:20-alpine AS node20
FROM php:8.2-fpm-alpine

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

# Install node
COPY --from=node20 /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node20 /usr/local/bin/node /usr/local/bin/node
RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm

RUN mkdir -p /home/devs
WORKDIR /home/devs

EXPOSE 9000
CMD ["php-fpm"]