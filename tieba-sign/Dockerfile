FROM python:alpine3.14
LABEL container.maintainer="xtoys <echoless@yeah.net>"

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    LANG=zh_CN.UTF-8 \
    TZ=Asia/Shanghai

COPY s6-overlay /

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk update -f \
    && apk --no-cache add -f \
       bash \
       tzdata \
       s6-overlay \
    && pip install -i https://mirrors.ustc.edu.cn/pypi/web/simple pip -U \
    && pip config set global.index-url https://mirrors.ustc.edu.cn/pypi/web/simple \
    && pip install --upgrade requests \
    && rm -rf /tmp/* \
    && rm -rf /root/.cache \
    && chmod -R +x /etc/cont-init.d \
    && chmod -R +x /etc/services.d

WORKDIR /scripts 
ENTRYPOINT ["/init"]
