FROM php:8.1-apache

RUN apt-get -y update
RUN apt-get install -y libicu-dev postgresql-server-dev-all git zip libjpeg-dev libpng-dev zlib1g-dev
RUN docker-php-ext-install intl  
RUN docker-php-ext-install pdo_pgsql 
RUN docker-php-ext-configure gd --with-jpeg=/usr/include/ && \
    docker-php-ext-install gd
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY sistemas.conf /etc/apache2/sites-available/sistemas.conf

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    a2enmod rewrite && \
    a2dissite 000-default && \
    a2ensite sistemas && \
    service apache2 restart

WORKDIR /var/www/html

EXPOSE 80