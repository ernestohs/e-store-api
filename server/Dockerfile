FROM php:8.2-apache

RUN apt-get update && apt-get install -y git curl libxml2-dev zip unzip

WORKDIR /var/www/html

COPY composer.json ./

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN composer install --no-dev --optimize-autoloader --no-scripts

# Copy all php code
COPY . .

EXPOSE 80

RUN a2enmod rewrite

COPY .conf/apache.conf /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

CMD ["apache2-foreground"]
