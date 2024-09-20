---
title: centos7升级GCC版本
slug: centos-update-gcc
description: ""
date: 2024-09-20T09:35:36+08:00
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

在 CentOS 7 上升级 GCC 版本可以通过多种方法实现, 这里使用个人认为最简单的方式升级，`CentOS SCL`

## 环境信息

- Centos7
- gcc4.8.5 ->gcc8.3.1

## 安装SCL仓库

```bash
yum install centos-release-scl
```
## 配置SCL仓库源

由于scl源在国外，有时候安装很慢，这里把源换成国内阿里源

- 修改CentOS-SCLo-scl.repo

```bash
# 备份
mv /etc/yum.repos.d/CentOS-SCLo-scl.repo  /etc/yum.repos.d/CentOS-SCLo-scl.repo.bak
# 写入阿里源
vim /etc/yum.repos.d/CentOS-SCLo-scl.repo
```
内容如下：
```bash
[centos-sclo-sclo]
name=CentOS-7 - SCLo sclo
baseurl=https://mirrors.aliyun.com/centos/7/sclo/x86_64/sclo/
# mirrorlist=http://mirrorlist.centos.org?arch=$basearch&release=7&repo=sclo-sclo
gpgcheck=0
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SC
```
- 修改CentOS-SCLo-scl-rh.repo
```bash
# 备份
mv /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo  /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo.bak
# 写入阿里源
vim /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo
```
内容如下：
```bash
[centos-sclo-rh]
name=CentOS-7 - SCLo rh
baseurl=https://mirrors.aliyun.com/centos/7/sclo/x86_64/rh/
# mirrorlist=http://mirrorlist.centos.org?arch=$basearch&release=7&repo=sclo-rh
gpgcheck=0
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-SIG-SCLo
```
清理缓存
```bash
yum clean all
```
## 安装gcc8
```bash
yum install devtoolset-8
```
## 临时启用devtoolset-8
```bash
scl enable devtoolset-8 bash
```
这将启动一个新的` shell `会话，其中` gcc `将指向 `devtoolset-8 `提供的 GCC 版本
## 验证gcc版本
```bash
gcc --version
```
输出类似于：`gcc version 8.3.1 20190311 (Red Hat 8.3.1-3) (GCC)`

## 注意

使用scl是临时启用的shell，只有在当前shell中gcc版本才是8.3.1，不是全局生效的，不建议全局生效，因为不同软件的编译依赖gcc版本不同，使用scl能完美解决不同gcc版本的使用问题
