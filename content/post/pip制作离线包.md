---
title: pip制作离线包
slug: pip制作离线包
description: ""
date: 2024-08-26T17:29:34+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
categories:
  - 笔记
tags:
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

## 背景
1. 解决无网络环境下安装python包的问题
2. 解决跨架构下安装python包，如x86环境下载arm架构下的pip包
## 解决方案

### 在线下载包及其依赖
通过 [`PyPI官网](https://pypi.org/) 下载所需的包。这种方式对于没有依赖或依赖较少的包较为方便。但对于依赖众多的包，需要逐个下载，过程较为繁琐。

### 使用pip下载

1. **准备联网环境**

	首先确保有一个可以访问互联网的环境,最好是相同python版本和架构
	
2. **下载包及其依赖**：
   - 使用以下命令下载所需的单个包和它的所有依赖：
     ```bash
     pip3 download -d pip-package -i https://pypi.tuna.tsinghua.edu.cn/simple requests
     ```
   - 其中，`-d` 参数指定下载目录。
   - `-i` 参数指定使用清华镜像源以加速下载。
3. **跨架构安装**：
   - 对于需要在不同架构之间安装包的情况，首先在目标架构的环境下使用上述方法下载包。
   - 然后将下载好的包复制到目标环境中进行安装。

### 注意事项
- 确保下载的包与系统中Python的版本和架构相兼容。
- 如果遇到下载速度慢或失败的问题，可以尝试更换其他镜像源，如阿里云、中国科技大学等提供的镜像源。
- 在使用pip下载包时，注意检查网络连接，以免下载中断导致安装失败。

