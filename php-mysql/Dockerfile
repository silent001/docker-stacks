FROM php:8.0-apache

LABEL maintainer="silent@silentmecha.co.za"

# Change DocumentRoot
ENV APACHE_DOCUMENT_ROOT /var/www/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Create DocumentRoot
RUN mkdir -p ${APACHE_DOCUMENT_ROOT}; \
	chown -R www-data:www-data ${APACHE_DOCUMENT_ROOT}/../; \
	chmod -R 777 ${APACHE_DOCUMENT_ROOT}/../

RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN a2enmod rewrite \
	&& a2enmod headers

# Work directory
WORKDIR ${APACHE_DOCUMENT_ROOT}