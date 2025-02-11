# Gebruik de officiële PHP Apache image
FROM php:8.3-apache

# Installeer vereiste extensies en afhankelijkheden
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    curl \
    git \
    && docker-php-ext-configure gd \
    && docker-php-ext-install pdo pdo_mysql gd \
    && rm -rf /var/lib/apt/lists/*

# Installeer Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Zet root wachtwoord voor debugging (verander dit in productie!)
RUN echo "root:3706" | chpasswd

# Stel de werkmap in
WORKDIR /var/www/html

# Kopieer Laravel-bestanden
COPY .. /var/www/html/

# Geef Apache en PHP de juiste rechten
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
RUN chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache

# Voer database migraties en seeders uit bij opstarten
RUN chmod +x /var/www/html/docker-entrypoint.sh

# Expose port 80
EXPOSE 80

# Start Apache en voer Laravel setup uit
CMD ["bash", "/var/www/html/docker-entrypoint.sh"]
