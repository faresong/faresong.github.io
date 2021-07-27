---
key: charles-shadowrocket-sagernet
title: 通过 Shadowrocket、SagerNet 工具使用 Charles 代理
tags: charles
---

## 1. 前言

当对移动端 app 进行测试时，常常需要使用到 Charles 来查看、修改网络请求的数据。虽然 iOS 和 Android 都提供有 HTTP 代理的设置，但使用并不方便 (每次都需要到 Wi-Fi 填配置，不用了也要去取消，下一次要用还得重新填，有时还发生无网络问题，才发现 Charles 关了而系统代理没关)。另外，一些 App (比如 Flutter app) 也可能并不应用系统的 HTTP 代理。有了 Shadowrocket、SagerNet 等工具，配置好了就可以一键启动一键关闭了，且通过状态栏就能看到代理是否处于开启状态。

## 2. 环境介绍

Charles 代理地址：192.168.1.11:8887 (SOCKS端口，默认的 8889 与 qv2ray 的 HTTP Proxy 端口重复)

Server 接口地址：http://192.168.1.22:8080

iOS & Android 设备地址：192.168.1.88

Shadowrocket 版本：2.1.77 (1245)

SagerNet 版本：0.1-beta1 (v2ray-core: v4.37.2)

## 3. Shadowrocket

Shadowrocket 支持 Charles 的 HTTP 和 SOCKS 代理。

一般情况下 Shadowrocket 全局路由的「代理」模式就能实现全代理的效果，但「代理」模式也是绕开了局域网地址的，因此需要使用「配置」模式，在默认的配置文件的基础上，「编辑配置」-「通用」-「跳过代理」这里删除需代理的局域网段 192.168.0.0/16，再在「编辑配置」-「通用」-「添加规则」这里「类型」选择「IP-CIDR」，「选项」选择「PROXY」，「域名」填入需代理的网段 192.168.1.22/32 (该网段只有 1 个 IP 地址)，保存后再进行 app 测试，就应该可以在 Charles 看到 app 的发起的请求了。

## 4. SagerNet

SagerNet 支持 Charles 的 SOCKS 代理。

服务模式 (Service mode) 选择 VPN，建议设置分应用代理 (Apps VPN mode)，路由 (Route) 选择 All，这样就可代理特定 app 的所有流量 (包括局域网)。

Android 虽然很早就有 v2rayNG 这个工具，和 SagerNet 一样应该都是 v2ray-core 提供的 Socks 实现，但感觉它的 Socks 存在问题，尝试过但没能成功使用。