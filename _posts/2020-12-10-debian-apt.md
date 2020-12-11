---
key: debian-apt
title: Debian apt 软件包管理
tags: Linux
---

###### 显示已安装软件包

`apt list --installed`

`apt list --installed | grep unzip`  (例，下同)

###### 搜索软件包 

`apt search unzip`

###### 显示某个包的信息

`apt search unzip`

###### 显示某个包的依赖关系

`apt depends unzip`

###### 只使用 IPv4

`apt -o Acquire::ForceIPv4=true install unzip`

###### 只使用 IPv6

`apt -o Acquire::ForceIPv6=true install unzip`