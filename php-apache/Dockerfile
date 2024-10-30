FROM php:8.2-apache

# RUN apt-get update \
#     && apt-get install -y nano zip unzip git libicu-dev \
#     && docker-php-ext-configure intl \
#     && docker-php-ext-install intl \
#     && apt-get clean \
#     && rm -rf /var/lib/apt/lists/*

RUN apt-get update
RUN apt-get install -y \
    nano \
    git \
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
    mysqli

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

WORKDIR /var/www/html

#RUN composer create-project codeigniter4/appstarter app --prefer-dist --stability=stable --no-progress --no-interaction

# /app /var/www/html/

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