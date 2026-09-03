---
title: docker基础组件搭建
date: 2026-08-15
draft: true
author: JackyLee
tags:
categories:
  - 计算机
comment: true
cover:
#   image:
#   hidden: false
---

## 安装 dokcer

## 运行最简单的服务

```sh
docker run -d --name my-nginx -p 80:80 nginx:alpine
docker ps -a
```

## DNS 服务

- 我这边使用 `dnsmasq` 服务
- 我内网服务器的静态ip是 `192.168.1.94`
- 假设我想映射的域名是 myname.home

```sh
# 校验配置是否正确
docker exec dnsmasq dnsmasq --test

# ufw 配置
sudo ufw allow in from 192.168.1.0/24 to any port 53 proto tcp
sudo ufw allow in from 192.168.1.0/24 to any port 53 proto udp
```

### windows

然后在控制面板>网络>属性>ipv4更改DNS地址

如何验证？

```sh
# 指定域名服务器是 192.168.1.94
nslookup myname.home 192.168.1.94

# windows查看本机DNS服务器
ipconfig /all
```

> 如果不行就关闭

### linux

```sh
# 编辑文件
sudo vim /etc/resolv.conf

# 写入(第一条最重要)
nameserver 192.168.1.94
nameserver 223.5.5.5
nameserver 114.114.114.114
```

```ini
# 静态配置的 DNS 服务器
server=223.5.5.5
server=114.114.114.114

# 禁止读取 /etc/hosts，完全忽略本机 hosts 文件的内容
no-hosts

# 监听网卡
listen-address=0.0.0.0
listen-address=127.0.0.1

# 域名解析
address=/myname.home/192.168.1.94

# DNS 缓存大小
cache-size=1000
```

## Docker 自建网络

第一步：手动创建共享网络（只执行一次）

```sh
docker network create web-shared
```

名字随便，这里叫 `web‑shared`。

> 这个网络是全局 docker 网络，不属于任何一个 compose 项目。

## 反向代理 Caddy

```sh

```

## 参考资料
