FROM openjdk:8-alpine

LABEL maintainer="seata <jaychang1987@gmail.com>"

ARG FILE

ADD ${FILE} /

WORKDIR /seata

RUN set -x \
    && sed -i "s/http:\/\/dl-cdn.alpinelinux.org/https:\/\/mirrors.aliyun.com/g" /etc/apk/repositories \
    && apk update \
    && apk --no-cache add tzdata curl tini \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" >  /etc/timezone \
    && rm -rf /var/cache/apk/*
# 设置额外参数
ENV EXTRA_JVM_ARGUMENTS="-XX:MaxDirectMemorySize=1024M"
ENV HOST_ARG=""

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["sh","-c","/seata/bin/seata-server.sh ${HOST_ARG}"]
EXPOSE 8091
