FROM php:7.3-cli

ENV TZ=Etc/UTC
RUN echo "[Date]\ndate.timezone = \${TZ}" > /usr/local/etc/php/conf.d/timezone.ini
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

RUN mkdir -p /app /var/log/usm_abills
WORKDIR /app
