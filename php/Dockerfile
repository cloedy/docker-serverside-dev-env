FROM ubuntu:18.04

# Install Laravel dependencies
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        mysql-client \
        libpq-dev \
        libpng-dev \
        libzip-dev \
        libbz2-dev \
        php7.2 \
        php7.2-fpm \
        wget \
        net-tools \
        cron

# Install composer
COPY ./install-composer.sh /tmp
RUN chmod +x /tmp/install-composer.sh && /tmp/install-composer.sh
RUN mkdir /run/php

# Delete default php-fpm config
RUN sed -i '/listen = \/run\/php\/php7\.2-fpm\.sock/d' /etc/php/7.2/fpm/pool.d/www.conf
#RUN sed -i '/^;listen\.allowed_clients/d' /etc/php/7.2/fpm/pool.d/www.conf

RUN sed -i '/^;date\.timezone =/d' /etc/php/7.2/fpm/php.ini
RUN sed -i '/^;cgi.fix_pathinfo=1/d' /etc/php/7.2/fpm/php.ini
RUN sed -i '/^display_errors = stderr/d' /etc/php/7.2/fpm/php.ini

# The new config
RUN echo 'listen = php:9000' >> /etc/php/7.2/fpm/pool.d/www.conf
#RUN echo 'listen.allowed_clients = nginx' >> /etc/php/7.2/fpm/pool.d/www.conf

RUN echo 'date.timezone = Asia/Shanghai' >> /etc/php/7.2/fpm/php.ini
RUN echo 'cgi.fix_pathinfo=0' >> /etc/php/7.2/fpm/php.ini
RUN echo 'display_errors = stderr' >> /etc/php/7.2/fpm/php.ini

EXPOSE 9000
CMD ["php-fpm7.2", "-F"]

