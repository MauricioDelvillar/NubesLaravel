# Usar la imagen base oficial de PHP con soporte FPM
FROM php:8.1-fpm

# Instalar las dependencias necesarias
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libmcrypt-dev \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
# Configurar el directorio de trabajo
WORKDIR /var/www

# Copiar el contenido del proyecto al contenedor
COPY . /var/www

# Ejecutar composer install
RUN composer install --no-dev --optimize-autoloader

# Exponer el puerto 80 para servir la aplicación Laravel
EXPOSE 80

# Comando por defecto para ejecutar cuando el contenedor se inicie
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=80"]


