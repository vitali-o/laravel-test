FROM php:8.4-cli

# System deps + PHP extensions build deps
RUN apt-get update && apt-get install -y --no-install-recommends \
    git unzip curl ca-certificates \
    libpq-dev \
    libzip-dev \
    default-mysql-client \
    libmariadb-dev \
  && docker-php-ext-install -j"$(nproc)" pdo_pgsql pgsql pdo_mysql zip \
  && pecl install redis \
  && docker-php-ext-enable redis \
  && rm -rf /var/lib/apt/lists/*

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
