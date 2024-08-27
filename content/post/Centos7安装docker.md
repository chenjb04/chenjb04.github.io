---
title: Centos7安装docker
slug: centos-install-docker
description: ""
date: 2024-08-22T16:40:12+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
categories:
  - 笔记
tags:
  - Linux
  - Docker
---

<!-- 字段	介绍	默认值
description	文章简介	
image	特色图片	
comments	显示 / 隐藏评论区	true
license	文章协议 输入 false 可以隐藏	params.article.license.default
hidden	隐藏文章（不在首页，归档等页面显示，但是可以直接通过链接访问）	false
math	加载 KaTeX 脚本	
toc	显示 / 隐藏目录	params.article.toc
lastmod	最后更改时间	 -->

## 卸载旧版本docker
```bash
yum remove docker \
		  docker-client \
		  docker-client-latest \
		  docker-common \
		  docker-latest \
		  docker-latest-logrotate \
		  docker-logrotate \
		  docker-engine
```
## 安装依赖
```bash
yum install -y yum-utils
```
## 配置yum docker源
```bash
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
## 安装docker
```bash
 yum install docker-ce docker-ce-cli containerd.io
```
## 启动docker
```bash
systemctl start docker
```