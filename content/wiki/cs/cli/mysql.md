---
type: basic-note
title: mysql
author: JackyLee
create_time: 2025-09-24
update_time:
tags:
description:
---

## 连接

```sh
# 无密码
mysql
# 账号 + 密码: 密码一般在环境变量中
mysql -u root -p
# 修改配置
nvim "D:\Scoop\apps\mysql\current\my.ini"
```

## 环境变量

```sh
echo $env:MYSQL_USERNAME
echo $env:MYSQL_PASSWORD
```

## 参考资料
