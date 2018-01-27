FROM        alpine:3.7 as builder

ARG         VERSION=0.5.12

RUN         apk --no-cache add --virtual .build-deps \
                build-base \
                argp-standalone && \
            wget -q https://github.com/ar-/incron/archive/$VERSION.tar.gz -O - | tar xz && \
            ( \
                cd incron-$VERSION && \
                make -j$(nproc) && make install \
            ) && \
            apk del .build-deps

###

FROM        allanlei/kubectl as kubectl

###

FROM        alpine:3.7
LABEL       maintainer="Allan Lei <allanlei@helveticode.com>"

CMD         ["incrond", "--foreground"]

RUN         apk --no-cache add --virtual .run-deps \
                libstdc++ \
                bash
COPY        --from=builder /usr/local/sbin/ /usr/local/sbin/
COPY        --from=builder /usr/local/bin/ /usr/local/bin/
COPY        --from=builder /etc/incron.d/ /etc/incron.d/
COPY        --from=builder /var/spool/incron/ /var/spool/incron/
COPY        --from=kubectl /usr/local/bin/ /usr/local/bin/
