FROM php:7.2.34-apache

# Set timezone
ENV TZ Asia/Jakarta
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Update & install
RUN apt-get update -y && \
    apt-get install -y \
    libzip-dev \
    libicu-dev \
    zlib1g-dev \
    libpng-dev \
    nano

# Install PHP extension
RUN docker-php-ext-install pdo pdo_mysql mysqli intl zip opcache

# Install apache module
RUN a2enmod rewrite && \
    a2enmod ssl && \
    a2enmod proxy && \
    a2enmod proxy_http && \
    a2enmod proxy_wstunnel

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=. --filename=composer && \
    mv composer /usr/local/bin/

# Expose apache
EXPOSE 80
