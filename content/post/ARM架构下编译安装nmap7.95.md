---
title: ARM架构下编译安装nmap7.95
slug: arm-nmap-compile
description: ""
date: 2024-09-13T14:44:31+08:00
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
  - nmap
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

## 下载源代码
从nmap官方网站下载源代码:  [nmap](https://nmap.org/dist/),这里我下载的是`nmap-7.95.tar.bz2`(bzip2 压缩)

```bash
# 使用wget或curl下载源代码（此处为示例命令）  
wget https://nmap.org/dist/nmap-7.95.tar.bz2 
# 解压
bzip2 -cd nmap-7.95.tar.bz2 | tar xvf -
# 进入创建的目录
cd nmap-7.95
```
## 配置编译环境
在编译之前，运行` configure` 脚本来配置编译环境。
```
./configure
```
`./configure `中有几个重要的参数

- `--prefix=<directoryname>`
	决定了 Nmap 及其组件的安装位置
- `--without-zenmap`
	 此选项可不安装 Zenmap 图形GUI，zenmap依赖python环境
-  `--with-openssl=<directoryname>`
		指定OpenSSL库的位置
- `--with-libpcap=<directoryname>`
		指定Libpcap库的位置，用于捕获网络数据包。
- `--with-libpcre=<directoryname>`
		指定PCRE（Perl兼容正则表达式）库的位置。
- `--with-libdnet=<directoryname>`
		指定Libdnet网络库的位置，用于数据包操作。


这里我不需要可视化GUI，所以指定了--without-zenmap`

```bash
./configure --prefix=/usr/local/nmap7.95 --without-zenmap
```

没有报错即为成功

![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913172719.png)

### 可能遇到的问题

1. 缺失gcc


![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913172235.png)

安装一下
```bash
dnf install gcc
```
## 编译

```bash
make
```
如果没有make命令，需要安装一下
```bash
dnf install make
```
![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913172902.png)
### 可能遇到的问题

1.缺失gcc-c++


![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913172817.png)


安装
```bash
dnf install gcc-c++
```

注意: make 编译失败时，处理完错误后，需要`make clean`清理一下，在重新执行`make`

## 安装

```bash
make install
```
![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913172934.png)
## 验证

```
/usr/local/nmap7.95/bin/nmap --version
```
看到以下结果即为成功


![](https://cdn.jsdelivr.net/gh/chenjb04/img@main/blog/20240913173004.png)

如果希望在任何位置都能直接通过`nmap`命令访问Nmap，可以添加一个软链接到系统路径中。
```bash
ln -s /usr/local/nmap7.95/bin/nmap /usr/sbin/nmap
```
加入软链接后.可以在任何位置运行以下命令来检查Nmap版本 
```bash
nmap --version
```
