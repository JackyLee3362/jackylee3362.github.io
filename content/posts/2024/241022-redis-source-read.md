---
title: redis 源码阅读笔记
date: 2024-10-22
draft: true
author: JackyLee
tags:
categories:
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---

## RoadMap 路线图

- [x] WSL2 中编译 redis ➕ 2024-10-22 ✅ 2024-10-22
- [x] 运行 wsl2/redis ➕ 2024-10-22 ✅ 2024-10-22
- [x] debug wsl2/redis ➕ 2024-10-22 ✅ 2024-10-22

## FAQ

### 什么是二进制安全（Binary Safe）的？

c/cpp 中读取字符串 `"hello,\0world"` 的长度，会因为 `\0` 发生问题，就是二进制不安全的

- [Binary-safe - Wikipedia](https://en.wikipedia.org/wiki/Binary-safe)
- [什么是二进制安全 - 她和她的猫](https://her-cat.com/posts/2021/03/25/what-is-binary-safe/)

### 什么是 `__attribute__((__packed__))` （在 sds.h 中声明）？

- [C语言**attribute** ((**packed**))关键字自动字节对齐 - -零 - 博客园](https://www.cnblogs.com/-wenli/p/13056243.html)
- [C/C++ **attribute**((**packed**)) 用法與範例 | ShengYu Talk](https://shengyu7697.github.io/cpp-attribute-packed/)

### 什么是 `void*`？

给编译器的注释

- [C 语言中 void\* 详解及应用 | 菜鸟教程](https://www.runoob.com/w3cnote/c-void-intro.html)

## Ref 参考

- [Redis本地调试 | 你要如何衡量你的人生](https://weikeqin.com/2023/07/22/redis-debug/)
- [redis源码解析 — redis 源码解析 1.0 documentation](https://redissrc.readthedocs.io/en/latest/#id3)
- [Redis 设计与实现（第一版） — Redis 设计与实现](https://redisbook.readthedocs.io/en/latest/)
- [Using alignment modifiers - IBM Documentation](https://www.ibm.com/docs/en/xl-c-and-cpp-aix/16.1?topic=data-using-alignment-modifiers)
- [数据类型范围 | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/cpp/data-type-ranges?view=msvc-170)
- [C 库函数 – realloc() | 菜鸟教程](https://www.runoob.com/cprogramming/c-function-realloc.html)
- [C 库函数 – memcpy() | 菜鸟教程](https://www.runoob.com/cprogramming/c-function-memcpy.html)
- [huangzworks/annotated_redis_source: 带有详细注释的 Redis 2.6 源码](https://github.com/huangzworks/annotated_redis_source)
- [C语言中的vsnprintf函数 - 禅元天道 - 博客园](https://www.cnblogs.com/chanyuantiandao/p/16982478.html)

## 参考文献

- [huangzworks/annotated_redis_source: 带有详细注释的 Redis 2.6 源码](https://github.com/huangzworks/annotated_redis_source)
- [杞鋂 - 有哪些值得推荐的小型 C 语言开源项目？ - 知乎](https://www.zhihu.com/question/20792016/answer/1925516322286071844)
  - 概要: 想要真正掌握 C 语言，最好的方式就是从一个优秀的项目开始。Redis，这个只有几万行代码的内存数据库，堪称 C 语言项目的典范。 // Redis 中的简单字符串实现 typedef struct sdshdr { int len; // 字符串长度 int free; // 未使用的字节数 char buf[]; // 字符串数据 } sdshdr; // 创建新字符串 sds sdsnew(const char \*init) { size_t initlen = (init == NULL) ? 0 : strlen(init); return sdsnewlen(init, initlen); } [图片] Redis 的设计…
  - 点赞: 60

- [从一个事故中理解Redis（几乎）所有知识点 - 知乎](https://zhuanlan.zhihu.com/p/1384511904)
