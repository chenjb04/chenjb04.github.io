---
title: centos7编译安装Python3.12.6
slug: centos-compile-python3
description: ""
date: 2024-09-14T14:34:35+08:00
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
  - python
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

## 环境

- Centos7
- Python3.12.6

## 下载Python源码

访问Python的[官方网站](https://www.python.org/ftp/python/)，下载最新的源码包,这里下载的是Python3.12.6

```bash
wget https://www.python.org/ftp/python/3.12.6/Python-3.12.6.tgz
```
## 解压源码包
```bash
tar xzf Python-3.12.6.tgz
cd Python-3.12.6
```
## 编译安装
```bash
./configure --enable-optimizations --prefix=/opt/python3.12.6
```
- `--enable-optimizations` 选项用于启用额外的优化，使 Python 运行更快。
- `--prefix` 指定python安装目录
```bash
make altinstall
```
- `make altinstall`用于避免覆盖系统默认的 Python 版本。

### 可能遇到的问题

![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240919202751.png)

这是因为使用了`--enable-optimizations`,而gcc版本4.x比较低导致的，这里可以去掉这个参数编译，也可以升级gcc版本到8.x以上，建议升级gcc版本，参考升级gcc文章，[centos7升级GCC版本](https://lovecx330.online/p/centos-update-gcc/)

## 验证安装

```bash
/opt/python3.12.6/bin/python3.12
```
能够直接进入python shell
## 设置软链接
```bash
ln -s /opt/python3.12.6/bin/python3.12 /usr/bin/python3.12
```
设置软链接后，终端可以直接`python3.12`执行

## 设置pip

pip默认安装了，只需要设置下软链接即可
```bash
ln -s /opt/python3.12.6/bin/pip3.12 /usr/bin/pip3.12
```