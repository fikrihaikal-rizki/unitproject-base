FROM php:5.6.40-apache

# Set timezone
ENV TZ Asia/Jakarta
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Fix deprecation of debian stretch
RUN echo "deb http://archive.debian.org/debian stretch main contrib non-free" > /etc/apt/sources.list

# Update & install
RUN apt-get update -y && \
    apt-get install -y \
    libzip-dev \
    libicu-dev \
    zlib1g-dev \
    libpng-dev \
    nano
    wget

# Install PHP extension
RUN docker-php-ext-install gd pdo pdo_mysql mysql mysqli intl zip opcache

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

RUN wget https://golang.org/dl/go1.24.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go1.24.1.linux-amd64.tar.gz
RUN export PATH=$PATH:/usr/local/go/bin

# Expose apache
EXPOSE 85
