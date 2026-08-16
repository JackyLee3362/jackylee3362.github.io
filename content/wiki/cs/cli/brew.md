---
title: brew
date: 2025-11-18
draft: true
author: JackyLee
tags:
categories: 
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---


## 常用命令

```sh
tldr brew

# 安装软件包或安装包
brew install 软件包

# 更新三连
brew outdate
brew update
brew upgrade

# 列出所有已安装的软件或安装包 
brew list

# 显示软件包或安装包的信息
brew info 软件包
```

## 如何查找依赖项

查看软件包的可选依赖关系
有些软件包具有可选的依赖关系，可以使用 options 命令查看这些选项。例如：

```sh
brew options package_name
# 查找已安装的，依赖 xxx 的软件
brew uses --installed xxx
# 查找所有依赖 xxx 的软件
brew uses xxx
```

## 参考资料
