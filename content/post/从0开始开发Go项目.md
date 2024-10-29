---
title: "从0开始开发Go项目"
slug: "go-zero-start"
description: "" 
date: 2024-10-29T17:45:19+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false    
categories: [笔记]
tags: [Go]
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

以前一直在做python项目，没有系统学习过go语言，接触的go项目有限，最近一个新引擎需要go语言开发，所以从头开始记录一下，也算学习了。

## 下载

go语言更新迭代较快，推荐下载新一点的版本，直接官网下载即可

下载地址：[https://go.dev/dl/](https://go.dev/dl/)

注意：Go1.20以上不支持`win7`了，成功踩坑，官方声明：[https://go.dev/doc/go1.20#windows](https://go.dev/doc/go1.20#windows)
## 设置环境变量
go语言中有好几个关键的环境变量和概念
### GOPATH
- 定义：GOPATH 是一个环境变量，指定了 Go 工作空间的路径。工作空间包含三个子目录：src（源代码）、pkg（编译后的包对象）和 bin（可执行文件）。

- 作用: 在 Go 模块化之前，GOPATH 是管理 Go 项目和依赖的主要方式。所有的 Go 代码和依赖包都需要放在 GOPATH/src 下。

- 现状：Go推出了模块化go mod ，这个可以不用使用了
### GOROOT
- 定义：GOROOT 是一个环境变量，指向 Go 的安装目录。

- 作用：它包含 Go 的编译器、标准库和工具链。通常不需要手动设置 GOROOT，因为 Go 的安装程序会自动配置。
### GOPROXY
- 定义：GOPROXY 是一个环境变量，用于指定 Go 模块代理的地址。

- 作用：模块代理是一个缓存服务器，用于加速模块的下载和解决依赖。默认的 Go 模块代理是 https://proxy.golang.org。

- 自定义：你可以设置 GOPROXY 来使用其他代理服务，国内建议设置一下代理，不然就要科学上网了
```bash
go env -w GOPROXY=https://goproxy.cn,direct
```
### go.mod
- 定义：go.mod 是一个文件，位于 Go 模块的根目录中。
- 作用：它定义了模块的名称、Go 版本和依赖项。go.mod 文件记录了项目的直接依赖及其版本。
- 管理：使用 `go mod init` 创建，使用 `go get`、`go mod tidy` 等命令更新。
### go.sum
- 定义：go.sum 是一个文件，记录了模块依赖的校验和。
- 作用：它确保模块的完整性和安全性，防止依赖被篡改。go.sum 文件包含了所有直接和间接依赖的版本和校验和。
- 自动更新：每次运行 `go mod tidy` 或 `go get` 时，go.sum 会自动更新
### 总结
- GOPATH：传统的工作空间路径，主要用于存储缓存。
- GOROOT：Go 安装目录，通常不需要修改。
- GOPROXY：模块代理地址，加速模块下载。
- go.mod：模块文件，定义项目依赖。
- go.sum：校验和文件，确保依赖完整性。

## Go编辑器
推荐`GoLand`（偏重）和`vs code`（轻量）

推荐配置ssh远程开发
## 创建项目目录
```bash
mkdir my-go-project
cd my-go-project
```
## 初始化Go模块

```bash
go mod init my-go-project
```
这将创建一个 `go.mod` 文件，记录项目的模块路径和依赖项。
## 编写代码
创建一个简单的 Go 文件，例如 `main.go`，并编写一些基本代码：

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

## 运行代码
```bash
go run main.go

```

至此剩下的就是组织目录结构和编码了