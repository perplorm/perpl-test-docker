FROM php:8.4-cli

RUN apt-get update \
 && apt-get install -y \
        curl \
        postgresql-client \
        default-mysql-client \
        sqlite3 \
        git \
        libpq-dev \
        libxml2-dev \
        libzip-dev \
        sqlite3 \
        unzip \
\
 && pecl install xdebug \
 && docker-php-ext-enable xdebug \
 && docker-php-ext-install \
    intl xml zip \
    pdo_mysql \
    pgsql pdo_pgsql \
\
 && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php -r "copy('https://composer.github.io/installer.sha384sum', 'composer-setup.sha384sum');" \
 && php -r "if (hash_file('sha384', 'composer-setup.php') . \" *composer-setup.php\n\" === file_get_contents('composer-setup.sha384sum')) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); unlink('composer-setup.sha384sum');} echo PHP_EOL;"\
 && php composer-setup.php \
 && rm composer-setup.sha384sum composer-setup.php \
 && mv composer.phar /usr/local/bin/composer
 

COPY ./php-container-setup/php-propel.ini "$PHP_INI_DIR"/conf.d/php-propel.ini
COPY ./php-container-setup/bashrc /root/.bashrc
COPY ./php-container-setup/bash_aliases /root/.bash_aliases

WORKDIR /propel/
