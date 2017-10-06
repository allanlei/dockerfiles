FROM        redis as builder

ARG         VERSION=1.0.0
WORKDIR     /
RUN         apt-get update && \
            apt-get install -y \
                build-essential \
                curl
RUN         curl -sfL https://github.com/RedisLabsModules/rebloom/archive/v$VERSION.tar.gz | tar xz -C /
RUN         cd rebloom-$VERSION && \
            make

###

FROM        busybox

ARG         VERSION=1.0.0
ENV         LIBDIR /var/lib/redis/modules
WORKDIR     $LIBDIR
VOLUME      $LIBDIR
COPY        --from=builder /rebloom-$VERSION/rebloom.so $LIBDIR/rebloom.so
