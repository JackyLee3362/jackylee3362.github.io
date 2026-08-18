---
title: git-branch
date: 2026-08-19
draft: true
author: JackyLee
tags:
categories:
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---

## 分支命令

```sh
# 查看当前分支
git branch

# 显示所有分支
git branch --list

# 创建分支
git branch 分支名

# 让main分支强制指向head前3个提交
git branch -f main HEAD~3
```
