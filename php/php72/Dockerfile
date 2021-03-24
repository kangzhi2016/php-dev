FROM php:7.2-fpm

#my_run
RUN apt-get update \
    && apt-get install -y \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        #安装amqp必须的
        librabbitmq-dev \
        libssh-dev \
#    && docker-php-ext-configure \
#        gd \
#        --with-freetype-dir=/usr/include/ \
#        --with-jpeg-dir=/usr/include/ \
#        --with-png-dir=/usr/include \
#        --with-librabbitmq-dir=/usr/include \
    && docker-php-ext-install \
        gd \
        pdo_mysql \
        mysqli \
        sockets \
        gettext \
        bcmath

# 解决pecl 出错的问题
COPY ./ext/* /home/ext/

RUN pecl install /home/ext/redis-5.1.0.tgz \
    && pecl install /home/ext/xdebug-2.7.2.tgz \
    && pecl install /home/ext/amqp-1.10.2.tgz \
    && docker-php-ext-enable redis xdebug amqp

RUN rm -rf /home/ext
