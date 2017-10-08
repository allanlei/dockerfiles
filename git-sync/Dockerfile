FROM        alpine:3.6 as builder

RUN         apk --no-cache add --virtual .build-deps \
                curl

            # Install s6-overlay
RUN         curl -sfL https://github.com/just-containers/s6-overlay/releases/download/v1.20.0.0/s6-overlay-amd64.tar.gz | tar xz -C /

###

FROM        alpine:3.6

ENV         S6_BEHAVIOUR_IF_STAGE2_FAILS 2
ENV         S6_CMD_WAIT_FOR_SERVICES 1
ENV         SCHEDULE="* * * * *"

RUN         apk --no-cache add --virtual .run-deps \
                git \
                openssh-client \
                ca-certificates

VOLUME      /root/.ssh
WORKDIR     /data
ENTRYPOINT  [ "/init-with-args" ]

COPY        --from=builder / /
COPY        rootfs /
