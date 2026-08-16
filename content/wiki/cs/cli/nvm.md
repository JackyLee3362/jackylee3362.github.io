---
title: nvm
date: 2025-08-27
draft: true
author: JackyLee
tags:
  - 必装软件
categories:
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---

> tldr nvm

## 安装

```sh
scoop install nvm
brew install nvm
```

## 基础

查看已经安装的 node

```sh
# 列出远程
nvm ls-remote
# 列出当前已安装的
nvm ls
# 安装
nvm install <version>
# 默认版本
nvm alias default <version>
```

## 常用

nvm list

nvm list-remote

nvm list available

## 设置代理

nvm proxy http://127.0.0.1:7890

## 设置镜像

nvm node_mirror https://npmmirror.com/mirrors/node/

## 参考资料
