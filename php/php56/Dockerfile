FROM php:5.6-fpm

#说明：如果因为网络问题方式一无法安装，可用方式二代替
#方式一
# RUN apt-get update && apt-get install -y libmcrypt-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
#     && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#     && docker-php-ext-install gd \
#     && docker-php-ext-install mcrypt \
#     && docker-php-ext-install pdo_mysql \
#     && docker-php-ext-install mysqli \
#     && docker-php-ext-install sockets \
#     && docker-php-ext-install gettext \
#     && pecl install /home/ext/redis-4.2.0.tgz \
#     && pecl install /home/ext/xdebug-2.5.5.tgz \
#     && docker-php-ext-enable redis xdebug

#方式二
#解决 debian 报错的问题
#RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
#    echo "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
#
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
    && docker-php-ext-configure \
        gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
        --with-png-dir=/usr/include \
        --with-librabbitmq-dir=/usr/include \
    && docker-php-ext-install \
        gd \
        mcrypt \
        pdo_mysql \
        mysqli \
        sockets \
        gettext \
        bcmath

# 解决pecl 出错的问题
COPY ./ext/* /home/ext/

RUN pecl install /home/ext/redis-4.2.0.tgz \
    && pecl install /home/ext/xdebug-2.5.5.tgz \
    && pecl install /home/ext/amqp-1.10.2.tgz \
    && docker-php-ext-enable redis xdebug amqp

RUN rm -rf /home/ext



