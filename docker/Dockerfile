# 使用 Alpine Linux 作为基础镜像
FROM alpine:latest

# 设置元数据
LABEL maintainer="m-longggg"
LABEL description="Argosbx Proxy Service Container"
LABEL version="V25.10.5"

# 设置环境变量
ENV LANG=en_US.UTF-8
ENV HOME=/root
ENV AGSDIR=$HOME/agsbx
ENV PATH=$HOME/bin:$PATH

# 安装依赖包
RUN apk update && apk add --no-cache \
    bash \
    curl \
    wget \
    openssl \
    coreutils \
    util-linux \
    procps \
    grep \
    sed \
    gawk \
    xz \
    jq \
    tini \
    && rm -rf /var/cache/apk/*

# 创建必要的目录
RUN mkdir -p $HOME/bin $AGSDIR

# 设置工作目录
WORKDIR $HOME

# 复制脚本文件
COPY scripts/argosbx.sh $HOME/bin/agsbx
COPY scripts/start.sh $HOME/start.sh

# 设置执行权限
RUN chmod +x $HOME/bin/agsbx $HOME/start.sh

# 创建非root用户（安全考虑）
RUN adduser -D -s /bin/bash agsbx-user && \
    chown -R agsbx-user:agsbx-user $HOME

# 设置环境变量（供容器运行时使用）
ENV uuid=""
ENV vlpt=""
ENV vmpt="" 
ENV hypt=""
ENV tupt=""
ENV xhpt=""
ENV vxpt=""
ENV anpt=""
ENV arpt=""
ENV sspt=""
ENV sopt=""
ENV reym="apple.com"
ENV cdnym=""
ENV argo=""
ENV ARGO_DOMAIN=""
ENV ARGO_AUTH=""
ENV ippz=""
ENV warp=""
ENV name=""

# 暴露端口范围
EXPOSE 10000-65535

# 健康检查
HEALTHCHECK --interval=30s --timeout=10s --start-period=40s --retries=3 \
    CMD pgrep -f "agsbx/(s|x)" || exit 1

# 使用非root用户运行（注释掉，因为脚本需要root权限）
# USER agsbx-user

# 使用 tini 作为 init 进程
ENTRYPOINT ["/sbin/tini", "--"]

# 默认启动命令
CMD ["/root/start.sh"]
