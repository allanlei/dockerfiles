FROM        redis:alpine as builder

ARG         VERSION=1.1.0
WORKDIR     /
RUN         apk --no-cache add --virtual .build-deps \
                build-base \
                curl

RUN         curl -sfL https://github.com/RedisLabsModules/rebloom/archive/v$VERSION.tar.gz | tar xz -C /
RUN         make -C rebloom-$VERSION

###

FROM        busybox

ENV         VERSION=1.0.0
ENV         LIBDIR /var/lib/redis/modules
WORKDIR     $LIBDIR
VOLUME      $LIBDIR
COPY        --from=builder /rebloom-$VERSION/rebloom.so $LIBDIR/rebloom.so
