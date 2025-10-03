FROM php:8.1-fpm
RUN apt-get update && apt-get install -y --no-install-recommends \
    default-libmysqlclient-dev \
    libzip-dev \
    zip \
    unzip \
 && docker-php-ext-install mysqli pdo pdo_mysql \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

