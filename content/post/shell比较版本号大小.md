---
title: shell比较版本号大小
slug: shell-compare-version
description: 
date: 2024-08-28T17:11:01+08:00
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
  - shell
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
在shell脚本中比较版本号大小是一种常见的任务，尤其是在漏洞检测中，对比版本号，判断漏洞是否存在。版本号通常由主版本号、次版本号和补丁号组成，格式可能是`major.minor.patch`。有时，版本号可能还包括预发布标签（如alpha或beta）或构建元数据。

以下是一个示例shell脚本，用于比较两个版本号的大小：

```bash
#!/bin/bash

# 比较两个版本号的函数
compare_versions() {
    local version1=$1
    local version2=$2

    # 将版本号分割成数组
    IFS='.' read -r -a ver1 <<< "$version1"
    IFS='.' read -r -a ver2 <<< "$version2"

    # 获取最大数组长度
    local max_len=${#ver1[@]}
    if [ ${#ver2[@]} -gt $max_len ]; then
        max_len=${#ver2[@]}
    fi

    # 比较每一部分
    for ((i=0; i<max_len; i++)); do
        # 如果某个版本号部分不存在，则视为0
        local part1=${ver1[i]:-0}
        local part2=${ver2[i]:-0}

        if ((part1 > part2)); then
            return 1
        elif ((part1 < part2)); then
            return 2
        fi
    done

    return 0
}

# 示例版本号
version1="1.2.3"
version2="1.2.4"

# 调用比较函数
compare_versions "$version1" "$version2"
result=$?

# 输出比较结果
if [ $result -eq 0 ]; then
    echo "版本号 $version1 等于 $version2"
elif [ $result -eq 1 ]; then
    echo "版本号 $version1 大于 $version2"
else
    echo "版本号 $version1 小于 $version2"
fi
```
返回结果：
- 返回 `0` 表示两个版本号相等。
- 返回 `1` 表示第一个版本号大于第二个版本号。
- 返回 `2` 表示第一个版本号小于第二个版本号。
