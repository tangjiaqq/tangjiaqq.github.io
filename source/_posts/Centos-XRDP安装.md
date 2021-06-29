---
title: Centos_XRDP安装
date: 2021-03-05 13:05:34
tags: 
- 远程操作
description: 安装XRDP Windows系统远程图形化操作
categories: 
- Linux
---



```shell
# XRDP   Centos7 需要用户自行安装图形化操作界面
 yum -y install epel-release #添加源
 yum -y install xrdp
systemctl start xrdp && systemctl enable xrdp
# 配置防火墙
firewall-cmd --add-port=3389/tcp --permanent
firewall-cmd --reload
# 安装完成之后使用Windows的远程桌面即可远程控制Centos主机
```

