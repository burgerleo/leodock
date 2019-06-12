ARG PHP_VERSION
FROM php:${PHP_VERSION}-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install cron & editor
RUN apt-get install -y cron vim

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl3 libcurl3-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.6.0
RUN docker-php-ext-enable xdebug

# Install redis
RUN pecl install redis-4.0.1
RUN docker-php-ext-enable redis

# Install sqllite
RUN apt-get install -y apt-transport-https gnupg && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update -yqq && \
    # Install Dependencies
    ACCEPT_EULA=Y apt-get install -y unixodbc unixodbc-dev libgss3 odbcinst msodbcsql17 locales && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    # link local aliases
    ln -sfn /etc/locale.alias /usr/share/locale/locale.alias && \
    locale-gen && \
    # Install pdo_sqlsrv and sqlsrv from PECL. Replace pdo_sqlsrv-4.1.8preview with preferred version.
    pecl install pdo_sqlsrv sqlsrv && \
    docker-php-ext-enable pdo_sqlsrv sqlsrv && \
    php -m | grep -q 'pdo_sqlsrv' && \
    php -m | grep -q 'sqlsrv' 


# Install bcmath and zip extensionfor acureport
RUN docker-php-ext-install bcmath
RUN apt-get install libzip-dev -y && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip

# Other PHP7 Extensions
RUN apt-get -y install libsqlite3-dev libsqlite3-0 mysql-client
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install json

RUN apt-get -y install zlib1g-dev
RUN docker-php-ext-install zip

RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

RUN docker-php-ext-install mbstring
RUN docker-php-ext-install gettext

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

RUN apt-get install -y net-tools

RUN apt-get install -y ntp

# 網路校正時間指令
# sudo ntpdate watch.stdtime.gov.tw

# 設置時區
RUN /bin/cp /usr/share/zoneinfo/Asia/Taipei /etc/localtime \
    && echo 'Asia/Taipei' >/etc/timezone

# Enable apache modules
RUN a2enmod rewrite headers ssl

COPY vhost.conf /etc/apache2/sites-enabled/vhost.conf

EXPOSE 80