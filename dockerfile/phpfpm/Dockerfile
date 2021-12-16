FROM php:7.3-fpm

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN apt-get update && apt-get install -y \
  gzip \
  libbz2-dev \
  libfreetype6-dev \
  libicu-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng-dev \
  libsodium-dev \
  libssh2-1-dev \
  libxslt1-dev \
  libzip-dev \
  libjpeg-dev \
  lsof \
  default-mysql-client \
  libfreetype6-dev \
  zip

RUN docker-php-ext-configure gd --with-jpeg-dir --with-freetype-dir && \
  docker-php-ext-install gd
  
RUN docker-php-ext-configure zip \
  && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash

RUN composer self-update --1

RUN docker-php-ext-install \
  bcmath \
  bz2 \
  iconv \
  calendar \
  exif \
  gettext \
  intl \
  mbstring \
  mysqli \
  opcache \
  pcntl \
  pdo_mysql \
  soap \
  sockets \
  sodium \
  sysvmsg \
  sysvsem \
  sysvshm \
  xsl \
  zip

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app
RUN mkdir -p /var/www/html \
   && chown -R app:app /var/www

USER app:app
VOLUME /var/www
WORKDIR /var/www/html
