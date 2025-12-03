# ---------------------------------------
    #  Laravel 11 + PHP 8.4 + Composer
    # ---------------------------------------
    FROM php:8.4-fpm
    
    # ---------------------------------------
    #  System dependencies
    # ---------------------------------------
    RUN apt-get update && apt-get install -y \
        git \
        curl \
        zip \
        unzip \
        libpng-dev \
        libonig-dev \
        libxml2-dev \
        libzip-dev \
        libssl-dev \
        && docker-php-ext-install pdo pdo_mysql mbstring zip bcmath gd
    
    # ---------------------------------------
    #  Install Composer
    # ---------------------------------------
    COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
    
    # ---------------------------------------
    #  Set working directory
    # ---------------------------------------
    WORKDIR /var/www
    
    # ---------------------------------------
    #  Copy project files into container
    # ---------------------------------------
    COPY . .
    
    # ---------------------------------------
    #  Install PHP dependencies
    # ---------------------------------------
    RUN composer install --no-interaction --prefer-dist --no-dev --optimize-autoloader
    
    # ---------------------------------------
    #  Set permissions for Laravel
    # ---------------------------------------
    RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache \
        && chmod -R 775 /var/www/storage /var/www/bootstrap/cache
    
    CMD ["php-fpm"]
    