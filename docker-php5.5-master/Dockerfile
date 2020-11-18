# image à utiliser
FROM php:5.5.24-apache

RUN echo "LimitRequestLine 10000" >> /etc/apache2/apache2.conf

# Modifie la taille max des requetes GET
RUN sed -i 's/KeepAliveTimeout 5/KeepAliveTimeout 5\nLimitRequestLine 10000/g' /etc/apache2/apache2.conf

RUN apt-get update
RUN apt-get -y install php5-mysql
# RUN docker-php-ext-install mysqli

RUN apt-get update && \
            apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libzip-dev && \
            docker-php-ext-install mysql mysqli pdo_mysql mbstring zip && \
            docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/  &&  \
            docker-php-ext-install gd 

# On copie le php.ini du repertoire actuel dans le contenaire
COPY ./docker/php.ini /usr/local/etc/php
COPY ./docker/000-default.conf /etc/apache2/sites-enabled

# Installation d'XDEBUG
RUN yes | pecl install xdebug-2.5.5 \
    && echo -e "\rzend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/php.ini
    
# Activation des modules de base d'apache2
RUN a2enmod cache.load expires.load rewrite.load expires.load headers.load && \
	service apache2 stop && \
	service apache2 start

# Installation de composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# le repertoire qui contient les codes sources (attention : dans le contenaire, donc le repertoire à droite du mapping du docker-compose)
RUN chmod 777 /var/www -R
WORKDIR /var/www/

# RUN gulp --proxy "http://localhost/sabonglissime_boutique/"

