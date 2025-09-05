# Stage 1: Build dependencies
FROM php:8.2-fpm-alpine AS builder

RUN apk add --no-cache \
    libzip-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-install pdo pdo_pgsql zip

WORKDIR /app
COPY composer.json composer.lock ./
RUN composer install --no-dev --optimize-autoloader

# Stage 2: Runtime
FROM php:8.2-fpm-alpine

RUN apk add --no-cache \
    libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql

WORKDIR /var/www/html
COPY --from=builder /app/vendor /var/www/html/vendor
COPY . .

RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

CMD ["php-fpm"]
