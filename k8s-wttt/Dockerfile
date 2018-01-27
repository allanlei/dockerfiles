FROM        alpine:3.7
LABEL       maintainer="Allan Lei <allanlei@helveticode.com>"

RUN         apk --no-cache add --virtual .run-deps \
                incron && \
            apk --no-cache add --virtual .run-deps -X http://dl-cdn.alpinelinux.org/alpine/edge/testing \
                kubernetes

CMD         ["incrond", "--foreground"]

COPY        incron.allow /etc/incron.allow
