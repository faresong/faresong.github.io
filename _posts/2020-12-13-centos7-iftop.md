---
key: centos7-iftop
title: CentOS7 安装 iftop
tags: CentOS
---

## 1. 前言

iftop (全称应该是 interface top) 是查看网络实时流量的工具。

在 Debian 发行版下，可直接通过 `apt install iftop` 快速安装。

CentOS7 直接通过 `yum install iftop` 并没有找到。



通过查找资料，得知有2种安装方式：添加第三方源、编译安装。

## 2. 添加第三方源

第三方源对于 CentOS7 x86_64 系统的 iftop 的帮助界面：<https://centos.pkgs.org/7/repoforge-x86_64/iftop-1.0-0.pre3.el7.rf.x86_64.rpm.html>。提示如下:

**Install Howto**

```bash
# 1.Download latest rpmforge-release rpm from
	http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el7/en/x86_64/rpmforge/RPMS/
# 2.Install rpmforge-release rpm:
	rpm -Uvh rpmforge-release*rpm
# 3.Install iftop rpm package:
	yum install iftop
```

大概意思是访问第1步的链接，找到并下载以 rpmforge-release 开头的 rpm 包，本例是 [
rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm](http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el7/en/x86_64/rpmforge/RPMS/rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm)，通过第2步安装该 rpm 包 (相当于添加源)，再通过第3步命令安装 iftop。



## 3.编译安装

**据称是依赖**

```bash
yum install flex byacc libpcap ncurses-devel libpcap-devel
```

**编译工具**

```bash
yum install make gcc
```

**源码下载**

`http://www.ex-parrot.com/pdw/iftop/download/` 下载最新源码

```bash
mkdir iftop
cd iftop
# 下载源码包
wget http://www.ex-parrot.com/pdw/iftop/download/iftop-1.0pre4.tar.gz
# 解压
tar zxvf iftop-1.0pre4.tar.gz
cd iftop-1.0pre4
# 生成预编译文件 Makefile
./configure
# 编译
make
# 安装
make install
# 运行 (若提示 -bash: /usr/sbin/iftop: No such file or directory，可参考下一步)
iftop
# 使 PATH 环境生效 (若已安装成功但提示没有命令。或者重新连接 SSH 也行)
source /etc/profile
```

## 参考
[centos 7 iftop 安装及使用说明 | cnblogs.com](https://www.cnblogs.com/yyxianren/p/12400513.html)

[Linux下通过源码编译安装程序 | linuxidc.com](http://www.linuxidc.com/Linux/2015-03/114689.htm)

