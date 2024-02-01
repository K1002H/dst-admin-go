FROM ubuntu:22.04

LABEL maintainer="xxxxx"
LABEL description="DoNotStarveTogehter server panel written in golang.  github: https://github.com/hujinbo23/dst-admin-go"

# Install packages
RUN echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list && \
   # dpkg --add-architecture i386 && \
   # apt-get update && \
   # apt-get install -y lib32stdc++6 libgcc1 libcurl4-gnutls-dev:i386 wget screen procps
    dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install -y --no-install-recommends --no-install-suggests  \
        libcurl4-gnutls-dev:i386 \
        lib32gcc1 \
        lib32stdc++6 \
        libcurl4-gnutls-dev \
        libgcc1 \
        libstdc++6 \
        wget \
        ca-certificates \
        screen \
        procps \
        sudo \
        net-tools \
        iproute2 \
        openresolv \
        iputils-ping \
        wireguard-tools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && sed -E -i 's/^(\s*)(.*sysctl -q net.ipv4.conf.all.src_valid_mark=1)/\1# \2/' /usr/bin/wg-quick

# 设置工作目录
WORKDIR /app

# 拷贝程序二进制文件
COPY dst-admin-go /app/dst-admin-go
RUN chmod 755 /app/dst-admin-go

COPY run.sh /app/run.sh
RUN chmod 755 /app/run.sh

COPY config.yml /app/config.yml
COPY dst_config /app/dst_config
COPY dist /app/dist
COPY static /app/static

# 内嵌源配置信息

EXPOSE 8082/tcp
EXPOSE 10888/udp
EXPOSE 10998/udp
EXPOSE 10999/udp

# 运行命令
ENTRYPOINT ["./run.sh"]
