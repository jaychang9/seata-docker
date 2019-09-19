# https://hub.docker.com/_/openjdk
FROM openjdk:8-alpine

# set label
LABEL maintainer="seata <jaychang1987@gmail.com>"

ARG SEATA_VERSION=0.8.1

WORKDIR /seata

RUN set -x \
    && sed -i "s/http:\/\/dl-cdn.alpinelinux.org/https:\/\/mirrors.aliyun.com/g" /etc/apk/repositories \
    && apk update \
    && apk --no-cache add tzdata curl tini bash \
    && wget  https://github.com/seata/seata/releases/download/v${SEATA_VERSION}/seata-server-${SEATA_VERSION}.tar.gz -P / \
    && tar -xzvf /seata-server-${SEATA_VERSION}.tar.gz -C / \
    && rm -rf /seata-server-${SEATA_VERSION}.tar.gz \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" >  /etc/timezone \
    && rm -rf /var/cache/apk/*
# 设置额外参数
ENV EXTRA_JVM_ARGUMENTS="-XX:MaxDirectMemorySize=1024M"

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["bash","-f","/seata/bin/seata-server.sh"]
EXPOSE 8091

