---
title: Docker命令大全
slug: Docker命令大全
description: 
date: 2024-08-22T17:14:23+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
categories:
  - 笔记
tags:
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

## docker启动所有已经停止的容器
```bash
docker start $(docker ps -a | awk '{ print $1}' | tail -n +2)
```
## docker删除正在运行的单个容器
```bash
docker rm -f <container_id>
```
## docker删除正在运行的所有容器
```bash
docker rm -f $(docker ps -q)
```
