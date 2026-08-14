---
title: 服务器常用命令
date: 2026-08-15
draft: true
author: JackyLee
tags:
categories:
  - 计算机
comment: true
cover:
#   image: https://w.wallhaven.cc/full/og/wallhaven-og61yl.png
#   hidden: false
---

## 本机信息

```sh
whoami
uname
```

## 权限

```sh
# 修改权限
sudo chown -R $user:user 待修改权限目录
sudo chown -R


chmod
```

## 网络

```sh
ip a
```

## 压缩与解压

```sh
# 压缩
tar -cvf xxx.tar 待压缩目录
# 解压
tar -xvf xxx.tar
```

## 编辑器

```sh
vim
```

## 网络下载

## 上传下载

sftp

```sh
sftp
```

scp

```sh
# 本地 -> 远程
scp 路径/到/本地文件 远程主机地址:路径/到/远程文件

# 远程 -> 本地
scp 远程主机地址:路径/到/远程文件 路径/到/本地目录
```

> scp、smb

## 容器

> 有必要单独出一篇文章

```sh
docker compose up -d
docker compose down
docker pull ...
docker run ...
docker ps
docker iamges
docker rmi
# 查看日志
docker compose logs -f nginx
# 进入容器内部
docker exec -it my-nginx sh

docker save -o xxx.tar
docker load -i xxx.tar
```

## 同步

- rsync(增量同步)
- rclone
- syncthing(p2p双源)
- nextcloud
- samba(smb)
- scp/sftp

## 备份

todo

## 参考资料
