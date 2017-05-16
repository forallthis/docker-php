FROM php:7.1.4-fpm-alpine
MAINTAINER lijing <179927545@qq.com>


#basic tools
ARG BASIC_TOOLS="\
	vim bash curl grep tzdata \ 
	"

#build dependence
ARG BUILD_DEPS="\
	build-base autoconf linux-headers readline-dev \ 
    freetype libjpeg-turbo libpng libmcrypt libwebp \
    curl-dev freetype-dev openssl-dev \ 
    libjpeg-turbo-dev libpng-dev libwebp-dev libmcrypt-dev libaio-dev \
	"

RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.4/main" >> /etc/apk/repositories \
	&& echo "http://mirrors.ustc.edu.cn/alpine/v3.4/community" >> /etc/apk/repositories \ 
	&& apk update && apk upgrade \ 
	&& apk add ${BASIC_TOOLS} \
    && apk add --no-cache --virtual .build-deps \ 
		${BUILD_DEPS} \
    && docker-php-ext-install opcache \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo_mysql mysqli \
	&& sed -i "s/struct sigaction {/#ifndef __sighandler_t \ntypedef void (*__sighandler_t)(int);\n#endif\nstruct sigaction\n{/g" /usr/include/signal.h \
	&& sed -i "s/union {void (*sa_handler)(int)/__sighandler_t sa_handler/g" /usr/include/signal.h \
	&& sed -i "s/ -n / /" `which pecl` \
    && pecl install redis \
    && pecl install mongodb \
    && pecl install swoole \
	&& apk del .build-deps \
	&& rm -rf /var/cache/apk/* \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

ADD php.ini /usr/local/etc/php/
