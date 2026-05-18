FROM jenkins/jenkins:2.528.3-lts-jdk17

# 切换到 root 用户来安装系统级软件
USER root

# 替换为清华大学 Debian 镜像源 (加速下载)，并安装 maven
RUN sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list.d/debian.sources || \
    sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y maven && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 安装完成后切换回 root 或 jenkins 用户
# (因为你原来的 compose 里写了 user: "0:0"，这里保持 root 身份运行以匹配你的挂载权限需求)
USER root