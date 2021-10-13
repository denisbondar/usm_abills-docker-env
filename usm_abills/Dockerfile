FROM php:7.4-cli-alpine
RUN mkdir -p /app /var/log/usm_abills
RUN docker-php-ext-install -j$(nproc) mysqli
WORKDIR /app
CMD [ "php", "usm_abills.php" ]