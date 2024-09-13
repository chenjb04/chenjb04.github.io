---
title: Python 列表删除元素
slug: python-list-remove
description: ""
date: 2024-09-03T19:28:27+08:00
image: 
math: 
license: CC BY-NC-ND
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
在python中删除列表中元素是比较常见的操作，删除的方法也比较多，这里列一下最常见的做法

## pop方法

`pop()`方法用于删除指定位置的元素，默认删除最后一个元素，返回值为该元素。如果索引超出范围，引发`IndexError`异常
```python
l = ['zhangsan', 'lisi', 'wangwu', 'zhaoliu']

# 删除索引为1的元素
remove_element = l.pop(1)
print(remove_element)   # lisi
print(l)  # ['zhangsan', 'wangwu', 'zhaoliu']

# 删除最后一个元素
remove_element = l.pop()
print(remove_element)   # zhaoliu
print(l)  # ['zhangsan', 'wangwu']

# 删除超过索引的元素
remove_element = l.pop(10) # IndexError: pop index out of range
```
注意：
- 需要知道要删除元素的指定索引位置。
- 索引超出范围，会抛出异常

使用场景

	适用于需要删除特定位置元素的场景，尤其是删除最后一个元素时。
## remove方法

`remove()`方法用于删除匹配到的第一个元素，无返回值。如果要删除的元素不存在，引发`ValueError`异常
```python
l = ['zhangsan', 'lisi', 'wangwu', 'zhaoliu', 'lisi']

# 删除lisi
l.remove('lisi')
print(l)  # ['zhangsan', 'wangwu', 'zhaoliu', 'lisi']

# 删除不存在的元素
l.remove('xxx')  # ValueError: list.remove(x): x not in list
```
注意：
- `remove`只会删除第一个匹配到的元素，如果有多个相同的元素要删除，那么`remove`就不太适用
- 删除不存在的元素，会抛出异常

使用场景

	适用于删除已知值的元素，且列表中该值不重复或只需删除第一个匹配项的场景。
## del语句
`del`和`pop()`方法类似，都是用于删除指定索引位置的元素，但是`del`更灵活一些，可以删除指定位置的切片，索引超出范围，会引发`IndexError`异常

```python
l = ['zhangsan', 'lisi', 'wangwu', 'zhaoliu', 'lisi']

# 删除索引为1的元素
del l[1]
print(l)  # ['zhangsan', 'wangwu', 'zhaoliu', 'lisi']

# 删除索引0-2的切片
del l[0:2]
print(l)  # ['zhaoliu', 'lisi']

# 删除不存在的索引
del l[100]
print(l)  # IndexError: list assignment index out of range
```
注意：
- 要知道要删除元素的指定索引位置
- 索引超出范围，会抛出异常

使用场景

	适用于删除特定位置或范围内的元素。

## 列表推导式

可以创建一个新列表，用于删除想删除的元素，比较灵活

```python
l = ['zhangsan', 'lisi', 'wangwu', 'zhaoliu', 'lisi']

# 删除lisi
new_l = [element for element in l if element != 'lisi']
print(new_l)  # ['zhangsan', 'wangwu', 'zhaoliu']
```
注意：
- 这种方式不能原地删除，需要创建新列表，开辟新的内存空间
- 列表非常大的情况，效率比较低，内存占用比较大

使用场景

	适用于需要删除多个相同元素或复杂条件删除的场景。

## filter函数

`filter`函数和列表推导式方式很像，但是`filter`函数是一个迭代器，内存效率高，处理大数据集时更高效
```python
l = ['zhangsan', 'lisi', 'wangwu', 'zhaoliu', 'lisi']

# 删除lisi
new_l = list(filter(lambda x: x != 'lisi', l))
print(new_l)  # ['zhangsan', 'wangwu', 'zhaoliu']
```
注意：
- 这种方式不能原地删除，需要创建新列表，开辟新的内存空间

使用场景

	适用于需要删除多个相同元素或复杂条件删除的场景，尤其是处理大数据集时。


## 总结

| 方法       | 使用场景                                     | 优点                         | 缺点                                                 |
| ---------- | -------------------------------------------- | ---------------------------- | ---------------------------------------------------- |
| `pop`      | 删除特定位置元素，尤其是最后一个元素         | 操作简单，返回被删除的元素   | 需要知道索引，索引超出范围会抛出异常                 |
| `remove`   | 删除已知值的元素                             | 不需要知道索引               | 只能删除第一个匹配项，删除不存在的元素会抛出异常     |
| `del`      | 删除特定位置或范围内的元素                   | 可以删除切片，灵活性高       | 需要知道索引，索引超出范围会抛出异常                 |
| 列表推导式 | 删除多个相同元素或复杂条件删除               | 灵活性高                     | 需要创建新列表，内存占用较大，处理大数据集时效率较低 |
| `filter`   | 删除多个相同元素或复杂条件删除，处理大数据集 | 内存效率高，适合处理大数据集 | 需要创建新列表，不能原地删除                         |
