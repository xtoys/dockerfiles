ARG ALPINE_VERSION
FROM alpine:${ALPINE_VERSION}

ENV SHELL=/bin/bash \
    TZ=Asia/Shanghai \
    PS1="\u@\h:\w \$ "

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --no-cache --update bash tzdata s6-overlay \
    && rm -rf /tmp/* \

ENTRYPOINT ["/init"]