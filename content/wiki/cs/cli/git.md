---
title: git
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

## 子命令

[[git-config]]

## 常用命令

```sh

# 初始化
git init

# 添加到暂存区
git add .
# 从暂存区移除
git rm --cached [文件]

# 提交
git commit -m
# 推送
git push
# 拉取
git pull
# 切换分支
git checkout
# 切换分支
git switch
# 查看状态
git status
# 查看状态(简洁版)
git status -s

# 查看仓库创建了多久
git log --reverse
# 查看仓库大小
git count-objects -vH
```

[[git-init]]
[[git-add]]
[[git-branch]]


## FAQ

### git如何对历史搜索

### 本地 Git 仓库删除大 object

- [Git - git-gc Documentation](https://git-scm.com/docs/git-gc/zh_HANS-CN)
- [git仓库清理--"保姆级"教程这是一篇关于Git仓库清理的文章; 或许你现在还用不到里面的操作;但是看完保证你会有不少 - 掘金](https://juejin.cn/post/7024922528514572302)

最简单的方法，删除远程仓库，重新上传并重新提交，缺点是会丢失历史数据，

2025-09-27 由于之前加入 rime-ice 仓库，导致仓库过大，只好按照这个方法

- [git项目大小优化笔记,删除历史提交中的大文件 - 凉游浅笔深画眉 - 博客园](https://www.cnblogs.com/fuhua/p/15527023.html#git%E9%A1%B9%E7%9B%AE%E5%A4%A7%E5%B0%8F%E4%BC%98%E5%8C%96%E7%AC%94%E8%AE%B0%E5%88%A0%E9%99%A4%E5%8E%86%E5%8F%B2%E6%8F%90%E4%BA%A4%E4%B8%AD%E7%9A%84%E5%A4%A7%E6%96%87%E4%BB%B6)

- [git仓库清理--"保姆级"教程这是一篇关于Git仓库清理的文章; 或许你现在还用不到里面的操作;但是看完保证你会有不少 - 掘金](https://juejin.cn/post/7024922528514572302)

### git 文件名大小写敏感

> 2025-03-22 clone joyful-pandas 遇到

![20250322002110-2025-03-22](https://assets-1302294329.cos.ap-shanghai.myqcloud.com/2025/md/20250322002110-2025-03-22.png)

原因是 windows 系统大小写不敏感，而 git 大小写敏感

- [Windows 大小写不敏感导致的 git 冲突 | Finisky Garden](https://finisky.github.io/git-is-case-sensitive-while-file-system-is-not/)

### git CR/CRLF 是怎么解决的？

### 前言

平常使用 `git add .` 或者 `git push|pull|clone` 等命令，已经无法满足各种奇怪的需求了，

在使用 Github 的时候，由于对【本地分支】和【远程分支】理解不够深刻，难免会出现各种问题

所以本文章持续记录使用 Git 时遇到的各种复杂场景

### 1 本地分支相关

#### 1.1 签出会覆盖本地修改

场景描述：

通常我会在 `dev` 分支上操作，然后细粒度地提交 commit，上传到 github 上形成一个 pull-request，然后 `main` 再接受 pr，合并成一个

但是有时候会忘记切换分支（比如现在就是），直接在 main 上更改

在 vscode 的状态栏就会出现 `*`，此时想换到 `dev` 分支

直接切换会出现

!签出会覆盖本地修改的图片

该提示下的三个选项分别是什么意思呢？

1. 储藏并签出：希望【暂存区】仍然在当前分支，然后切换到另一个分支
2. 迁移更改：希望将【暂存区】的内容切换到另一个分支，可能要处理冲突问题
3. 强制签出：（不推荐）直接放弃当前分支（比如 `main`）未提交的 `commmit`，然后切换为分支 `dev`

所以该场景我们需要的是【迁移更改】
