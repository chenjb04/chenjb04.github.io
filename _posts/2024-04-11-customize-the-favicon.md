---
title: centos7安装docker
date: 2024-04-24 9:42:38 +0800
categories: [centos, docker]
tags: [docker]     # TAG names should always be lowercase
---


```bash
# 卸载旧版本
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
# 安装
sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

 sudo yum install docker-ce docker-ce-cli containerd.io
# 启动
sudo systemctl start docker
```
