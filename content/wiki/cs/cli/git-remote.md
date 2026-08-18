---
title: git-remote
date: 2025-08-03
draft: true
author: JackyLee
tags:
categories:
cover:
  # image: 图片链接
  # alt: 文字内容
comment: true
---

## 取消关联远程分支

```sh
# 切换分支
git switch 分支
# 查看关联信息
git branch -vv
# 取消关联上游
git branch --unset-upstream
# 查看关联信息
git branch -vv
# git 本地新建远程对应分支
git checkout -b local-branch-name origin/remote-branch-name
```

## 删除远程分支

远程分支已删除，本地仍然保留远程分支，如何清理过期的分支

原因就是本地缓存了远程分支的信息，要删除本地缓存的已删除远程分支，可以使用以下 `git` 命令

```sh
git remote prune origin
```

## 参考资料
