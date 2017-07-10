FROM php:7.1.4-fpm

MAINTAINER lijing <97244081@qq.com>

COPY sh /var/pkg/sh

RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \ 
    && echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >/etc/apt/sources.list \
    && echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list \
    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list \
    && echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list \
	&& apt-get update \
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
		--no-install-recommends && rm -r /var/lib/apt/lists/* \
	&& mkdir -p /var/pkg/php-modules \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install opcache \ 
	&& docker-php-ext-install pdo_mysql \
	&& pecl install redis \
	&& pecl install mongodb \
	&& pecl install swoole \
	&& pecl install channel://pecl.php.net/zookeeper-0.3.2 \
	&& /var/pkg/sh/install-librdkafka \
	&& pecl install rdkafka \
	&& /var/pkg/sh/install-phalcon \
	&& /var/pkg/sh/install-scws \
	&& rm -rf /var/pkg/* && rm -rf /tmp/* \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

COPY php.ini /usr/local/etc/php/
