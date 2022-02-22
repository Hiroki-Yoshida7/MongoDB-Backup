FROM node:8-alpine
MAINTAINER Hiroki Yoshida

RUN apk update && apk add tzdata mongodb-tools &&\ 
    cp /usr/share/zoneinfo/Europe/Prague /etc/localtime &&\ 
    echo "Europe/Prague" > /etc/timezone &&\ 
    apk del tzdata && rm -rf /var/cache/apk/*

CMD chown root:root /etc/crontabs/root && /usr/sbin/crond -f