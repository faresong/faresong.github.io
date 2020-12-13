---
key: axel-multi-connection
title: Linux 多线程下载工具 axel 
tags: Linux
---

## 1. 前言

 Linux 一般使用 wget 或 curl 来进行文件的下载，但似乎都只能单线程下载，在网络限制比较严格的情况下载总是很慢，这种情况下多线程下载工具总能有更好的速度表现。axel 就是一款支持多线程下载的工具。

## 2. Too many redirects

在使用 `apt install axel` 的安装下，有时候会出现 `Too many redirects`，因为链接发生了跳转，比如在某些软件官网的 Download 链接会跳转至他的 Github Release 下载。这是因为旧版本的 axel 未能支持链接跳转，比如 Debian 8 默认的版本 `2.4.0` 会出现 `Too many redirects`。

## 3. 源码编译安装

<https://github.com/axel-download-accelerator/axel> 下载 Release 的源码。

注意各个系统的依赖 Dependencies。再通过简单的 configure、make、make install 即可安装。安装前可先移除老版本 `apt remove axel`。

## 4. 使用

```bash
Axel 2.17.10 (linux-gnueabihf)
Usage: axel [options] url1 [url2] [url...]

--max-speed=x           -s x    Specify maximum speed (bytes per second)
--num-connections=x     -n x    Specify maximum number of connections
--max-redirect=x                Specify maximum number of redirections
--output=f              -o f    Specify local output file
--search[=n]            -S[n]   Search for mirrors and download from n servers
--ipv4                  -4      Use the IPv4 protocol
--ipv6                  -6      Use the IPv6 protocol
--header=x              -H x    Add HTTP header string
--user-agent=x          -U x    Set user agent
--no-proxy              -N      Just don't use any proxy server
--insecure              -k      Don't verify the SSL certificate
--no-clobber            -c      Skip download if file already exists
--quiet                 -q      Leave stdout alone
--verbose               -v      More status information
--alternate             -a      Alternate progress indicator
--help                  -h      This information
--timeout=x             -T x    Set I/O and connection timeout
--version               -V      Version information

Visit https://github.com/axel-download-accelerator/axel/issues to report bugs
```

## 参考
[介绍一款linux多线程下载工具axel（用以替代wget）| 评论中关于 Too many redirects 的原因 | segmentfault.com](https://segmentfault.com/p/1210000009861331)