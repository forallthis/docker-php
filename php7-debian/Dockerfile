FROM php:7.1.4

MAINTAINER lijing <97244081@qq.com>


COPY sh /var/pkg/sh

##RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
##    && echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >/etc/apt/sources.list \
##    && echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list \
##    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list \
##    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list \
RUN   apt-get update \
      && apt-get install -y \
		tar \
		wget \
		git \
		libssl-dev \
        libzookeeper-mt2 libzookeeper-mt-dev \
        libpcre3-dev \
        python \
        libmcrypt4 \
        libmcrypt-dev \
		tzdata \
        libzip-dev \
		##thrift begin 
        automake \
        bison \
        flex \
        g++ \
        libboost1.55-all-dev \
        libevent-dev \
        libtool \
        pkg-config \
        ##thrift end
		vim \
        sudo \
        --no-install-recommends && rm -r /var/lib/apt/lists/* \
	&& mkdir -p /var/pkg/php-modules \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install opcache \
    && docker-php-ext-install pdo_mysql \
    && pecl install zip \
    && pecl install redis \
    && pecl install mongodb \
    && pecl install swoole \
    && pecl install channel://pecl.php.net/zookeeper-0.3.2 \
    && /var/pkg/sh/install-librdkafka \
    && pecl install rdkafka \
    && /var/pkg/sh/install-phalcon \
    && rm -rf /var/pkg/* && rm -rf /tmp/* \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
	&& echo "Asia/Shanghai" > /etc/timezone \
   	&& curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && adduser -q admin \
    && sudo -u admin composer config -g repo.packagist composer https://packagist.phpcomposer.com \
    && cd /tmp \
    && wget http://mirror.bit.edu.cn/apache/thrift/0.10.0/thrift-0.10.0.tar.gz \
    && tar xvf thrift-0.10.0.tar.gz \
    && cd thrift-0.10.0 \
    && ./configure --with-php \
    && make \
    && make install \
    && cd /tmp \
    && rm -rf thrift-0.10.0 thrift-0.10.0.tar.gz


COPY php.ini /usr/local/etc/php/
