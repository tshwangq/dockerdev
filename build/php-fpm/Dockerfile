FROM php:7.1-fpm

MAINTAINER Qun Wang <tshwangq@gmail.com>
COPY . .
RUN cat  /etc/apt/sources.list
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak && mv sources.list /etc/apt/
RUN cat  /etc/apt/sources.list
#RUN echo "Asia/Shanghai" > /etc/timezone
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get clean && apt-get update -y
RUN apt-get install -y \
    libmcrypt-dev \
    libicu-dev \
    libpq-dev \
    libbz2-dev \
    git \
    unzip \
    curl \
    mc \
    wget \
    libevent-dev \
    librabbitmq-dev
RUN docker-php-ext-install iconv \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install intl \
    && docker-php-ext-install pgsql pdo pdo_pgsql \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install opcache \
    && docker-php-ext-enable opcache
# Install GD
RUN apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev
RUN docker-php-ext-configure gd \
    --enable-gd-native-ttf \
    --with-freetype-dir=/usr/include/freetype2 \
    --with-png-dir=/usr/include \
    --with-jpeg-dir=/usr/include \
    && docker-php-ext-install gd \
    && docker-php-ext-enable gd

RUN cp php.ini /usr/local/etc/php/
RUN cp ixed.7.1.lin  /usr/local/lib/php/extensions/no-debug-non-zts-20160303
RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
