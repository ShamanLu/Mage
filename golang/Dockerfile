FROM golang:latest

LABEL maintainer="phillu <phillu@outlook.com>"

ENV GOPROXY https://goproxy.cn,direct

# 设置国内源
ARG CHANGE_SOURCE=false
RUN if [ ${CHANGE_SOURCE} = true ]; then \
    sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list && \
    sed -i 's/security-cdn.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list \
;fi

# 安装必要的软件包和依赖包
USER root
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    curl \
    zip \
    unzip \
    make \
    git \
    vim \
    screen

# 安装 goctl
USER root
RUN GOPROXY=https://goproxy.cn/,direct go install github.com/go-kratos/kratos/cmd/kratos/v2@latest

# 安装 protoc
USER root
RUN curl -L -o /tmp/protoc.zip https://github.com/protocolbuffers/protobuf/releases/download/v25.1/protoc-25.1-linux-x86_64.zip && \
    unzip -d /tmp/protoc /tmp/protoc.zip && \
    mv /tmp/protoc/bin/protoc $GOPATH/bin

# 安装 protoc-gen-go
USER root
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@latest

# 安装 protoc-gen-go-grpc
USER root
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# $GOPATH/bin添加到环境变量中
ENV PATH $GOPATH/bin:$PATH

# 清理垃圾
USER root
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

# 设置工作目录
WORKDIR /usr/src/code

EXPOSE 8000
# EXPOSE 8001
# EXPOSE 8002
# EXPOSE 8003
EXPOSE 9000
# EXPOSE 9001
# EXPOSE 9002
# EXPOSE 9003
