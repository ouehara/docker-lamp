FROM diwamoto0118/php7.3-apache-alpine:latest

# 必要ファイルのコピー
COPY ./web/php7/php.ini /usr/local/lib/php.ini
COPY ./web/php7/httpd.conf /etc/apache2/
COPY ./web/vhost.conf /etc/apache2/conf.d/

RUN apk update && apk upgrade && apk --no-cache add tzdata vim git bash \
    # timezoneの設定
    && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && apk del tzdata \
    # docker-machine用の設定 マウントした際にuseridが変更される為
    && addgroup -S -g 50 dapacheg && adduser -S -u 1000 -g 50 dapache \
    # xdebugの設定
    && mkdir /run/apache2 \
    && chmod 777 /run/apache2 \
    # mailhogの設定
    && curl -sSLO https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 \
    && chmod +x mhsendmail_linux_amd64 \
    && mv mhsendmail_linux_amd64 /usr/local/bin/mhsendmail \
    # Composerのinstall
    && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer \
    # 無駄ファイルを削除
    && rm -rf /tmp/* /var/cache/apk/*

