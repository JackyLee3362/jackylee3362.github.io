---
title: 我的家庭服务器
date: 2026-08-15T00:19:26+08:00
draft: true
author: JackyLee
tags:
categories:
comment: true
cover:
#   image: https://w.wallhaven.cc/full/og/wallhaven-og61yl.png
#   hidden: false
---

## 选择操作系统

市面上的服务器操作系统主要包含

- Debian 系列: 纯净
- Ubuntu Server: 常用，生态全
- RHEL 系列: 比如 CentOS，商用稳定
- Windows Server 系统
- FreeBSD: 闭源，高性能

这边我选择使用 Debian 13，联网安装

```sh
# 查看用户
whoami

# 查看系统
uname -a
```

> 参考这篇文章 [Debian系统最小化安装教程 | DebNAS](https://kekylin.github.io/debnas-docs/guide/debian-minimal-installation/)
> 语言记得选英文

## 选择烧录工具

准备一个u盘

常见的烧录工具

- rufus: 45k⭐ <https://github.com/pbatard/rufus>
- etcher: 34.2k⭐ <https://github.com/balena-io/etcher>

中间如果u盘有问题

```sh
diskpart
list disk
# ⚠️ 找到你的U盘，记下磁盘号（比如 Disk 4）
select disk 4
# ⚠️ 这步操作非常危险，不熟悉的朋友不要做
clean
create partition primary
format fs=fat32 quick
assign
exit
```

## 安装 sudo 服务

```sh
# 进入 root
su -

# 下载 sudo
apt install sudo

# 加入用户组
adduser 你的用户名:你的用户组 sudo
adduser myname:myname sudo

# 重启
reboot

# 测试
sudo whoami

# 查看你是哪个组
groups yourname
```

## 下载 vim

```sh
apt install vim
```

> 简单的 vim 配置见文末附录

## 设置静态 IP

```sh
# 查看自己的网卡
ip a

# 设置静态ip
# 将下面的配置更新进去 
sudo vim /etc/network/interfaces


# 重启网络
sudo systemctl restart networking

# 验证是否生效
ip a
ip route
ping baidu.com
```

```conf
auto lo
iface lo inet loopback

auto 网卡名 
iface 网卡名 inet static
    address 你的静态地址,比如 192.168.1.95
    netmask 255.255.255.0
    gateway 192.168.1.1
    ... 其他不用管
```

## 安装 ssh 服务

```sh
# .ssh文件夹权限必须700
chmod 700 ~/.ssh
# authorized_keys 公钥文件权限必须600
chmod 600 authorized_keys
sudo apt install openssh-server -y
# 在本机生成公钥后，放到服务器的 .ssh/authorized_keys 中

# 设置禁止 root 登录
# 设置禁止密码登录
vim /etc/ssh/sshd_config
# PermitRootLogin prohibit-password 改为 PermitRootLogin no
# PasswordAuthentication no

# 重启
systemctl restart ssh
```

## 设置不休眠

```sh
# 阻止休眠功能
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
# 测试休眠
systemctl status sleep.targetsystemctl status sleep.target
# 恢复休眠功能
sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

## 附录

### .vimrc 配置

```txt
" 设置在光标距离窗口顶部或底部一定行数时，开始滚动屏幕内容的行为
set scrolloff=5
set cursorline

"Vim 会在您输入搜索模式的过程中逐步匹配并高亮显示匹配的文本
set incsearch

" 禁用命令超时 / 禁用映射超时
set notimeout

"--在搜索时忽略大小写
set ignorecase

"--将搜索匹配的文本高亮显示
set hlsearch

" 设置显示行号(或者set nu) , 取消用set nonumber/nu!
set number
set relativenumber

" 剪贴板设置
set clipboard=unnamed

" 行间移动
noremap J <C-d>
noremap K <C-u>

" 行内移动
noremap H ^
" noremap L $ 取消 $
noremap L g_

" 复制
noremap sp "0p
```
