FROM alpine:3.14
LABEL container.maintainer="xtoys <echoless@yeah.net>"

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    LANG=zh_CN.UTF-8 \
    TZ=Asia/Shanghai \
    WORKSPACE=/store 

COPY --from=xtoys/loop:latest / /
COPY s6-overlay /

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk update -f \
    && apk add -f \
       git \
       bash \
       nodejs \
       npm \
       wget \
       curl \
       nano \
       tzdata \
       python3 \
       py3-pip \
       openssh \
       s6-overlay \
    && npm install -g npm@latest \
    && npm config set registry https://registry.npm.taobao.org \
    && pip install -i https://mirrors.ustc.edu.cn/pypi/web/simple pip -U \
    && pip config set global.index-url https://mirrors.ustc.edu.cn/pypi/web/simple \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && rm -rf /var/cache/apk/* \
    && rm -rf /root/.npm \
    && rm -rf /root/.cache \
    && chmod +x /usr/bin/loop \
    && chmod -R +x /etc/cont-init.d \
    && chmod -R +x /etc/services.d

WORKDIR $WORKSPACE
ENTRYPOINT ["/init"]
