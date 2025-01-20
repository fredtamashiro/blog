FROM php:8.3-fpm

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip \
    && docker-php-ext-install intl opcache pdo mysqli pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

# Install Vim
RUN apt install -y vim    

# Install Node.js and npm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt install -y nodejs

WORKDIR /var/www/blog

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN wget https://get.symfony.com/cli/installer -O - | bash
RUN curl -sS https://get.symfony.com/cli/installer | bash

# Copie os arquivos da aplicação
COPY . /var/www/blog

# Instale as dependências do Node.js e execute o build do Vite
# RUN cd /var/www/blog && npm install && npm run build

# Crie os diretórios necessários
# RUN mkdir -p /var/www/blog/storage /var/www/blog/bootstrap/cache /var/www/blog/bootstrap/cache

# Ajuste as permissões
# RUN chown -R www-data:www-data /var/www/blog/storage /var/www/blog/bootstrap/cache
# RUN chmod -R 775 /var/www/blog/storage /var/www/blog/bootstrap/cache