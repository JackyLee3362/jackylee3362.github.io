---
title: Hugo 简易教程
date: 2024-04-03T11:00:30+08:00
draft: false
author: JackyLee
tags:
  - go
  - hugo
  - 教程
categories:
  - 计算机
cover:
  image: https://assets-1302294329.cos.ap-shanghai.myqcloud.com/2026/md/20260728162921.png
  hidden: false
comment: true
---

## 介绍

Hugo 是一个由 Go 语言编写的静态博客框架

- 仓库地址: [Hugo - github](https://github.com/gohugoio/hugo)

## 安装

```sh
# windows
scoop install hugo
# unix
brew install hugo
```

## 配置文件

默认的配置文件

## 主题

默认使用 PapaeMod 这个主题

[sample-config.yml | hugo-PaperMod Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#sample-configyml)

## 更新工作流

- 第一步: 生成文章模板

```shell
# 默认模板
hugo new post/xxx.md

# 指定模板
hugo new --kind [archetypes] post/xxx.md
## 例如
hugo new --kind post post/whatever.md
```

- 第二步: 内容创作

- 第三步: 提交与发布

如果是草稿态，记得打开 `draft:true`

## FAQ

### Q1: 如果添加图片

第一种方案: 用图床

![崩坏星穹铁道](https://assets-1302294329.cos.ap-shanghai.myqcloud.com/2026/md/20260728162921.png)

第二种方案: 使用 index.md 方法，可以参考下文

[Hugo 博客插入图片的方法 | Cassius's Blog](https://www.yuweihung.com/posts/2021/hugo-blog-picture/)

### Q2: tag 和 category 区别

参考如下文章

[Hugo 框架中文文档 标签分类 - Andbible](https://www.andbible.com/post/hugo-content-management-taxonomies/#default-taxonomies)

```yaml
taxonomies:
  category: categories
  tag: tags
```

## 参考

[LoveIt](https://hugoloveit.com/zh-cn/)

[Cassius's Blog](https://www.yuweihung.com/)
