FROM httpd:2.4.35-alpine

MAINTAINER Isaac Henrique <isaachbnn@gmail.com>

RUN set -ex \
    && apk update \
    && apk add --no-cache bash \
    && rm -rf /tmp/*

CMD ["httpd", "-DFOREGROUND"]
