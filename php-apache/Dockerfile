FROM php:8.2-apache

RUN apt-get update
RUN apt-get install -y \
    nano \
    git \
    zlib1g-dev \
    libzip-dev \
    zip \
    curl \
    sudo \
    unzip \
    libicu-dev \
    libbz2-dev \
    libpng-dev \
    libjpeg-dev \
    libmcrypt-dev \
    libreadline-dev \
    libfreetype6-dev \
    g++

RUN docker-php-ext-install \
    bz2 \
    intl \
    bcmath \
    opcache \
    calendar \
    pdo_mysql \
    mysqli \
    gd \
    zip

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www/html \
    && composer self-update

COPY codeigniter.conf /etc/apache2/sites-available/

RUN a2enmod rewrite headers

RUN a2ensite codeigniter.conf \
    && service apache2 reload || true

RUN cd /etc/apache2/sites-available \
    && a2dissite 000-default.conf \
    && service apache2 reload || true

EXPOSE 80