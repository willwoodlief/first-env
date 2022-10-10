ARG TARGET_PHP_VERSION=8.1.10
FROM php:${TARGET_PHP_VERSION}-fpm as php_base

COPY --from=composer:2.4.2 /usr/bin/composer /usr/bin/composer

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions 
RUN install-php-extensions gd xdebug mysqli pdo_mysql curl zip bcmath luasandbox intl

RUN apt-get update && apt-get install -y \
    curl \
    dnsutils \
    gdb \
    git \
    htop \
    iproute2 \
    iputils-ping \
    libarchive-tools \
    ltrace \
    make \
    procps \
    strace \
    sudo \
    sysstat \
    unzip \
    vim \
    wget \
  && rm -rf /var/lib/apt/lists/*

FROM php_base as php_config

ARG TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo ${TZ} > /etc/timezone

ENTRYPOINT ["php-fpm"]
EXPOSE 9000