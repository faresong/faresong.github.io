---
key: nvm-nodejs
title: nvm 安装 nodejs 以及 yarn
tags: nodejs
---

## 1. 前言

nvm 设计用来管理 nodejs 版本，它本质上是一个 shell 脚本。

## 2. nvm 使用

[nvm 的 Github 项目页面](https://github.com/nvm-sh/nvm) 提供了安装的教程。可通过 curl 或 wget 下载。

**下载&安装**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

**使设置的环境变量生效**

```bash
source ~/.bash_profile
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

**常用命令**

```bash
# 列出所有 LTS 版本
nvm ls-remote --lts
# 显示当前版本
nvm current
# 切换版本
nvm use [版本号]
# 切换版本
nvm use [版本号]
# 安装
nvm install [版本号]
```

## 3. 安装 yarn

**npm 设置代理** (yarn 也将会使用 npm 的代理设置)

```ba&#39;sh
npm config set proxy=http://127.0.0.1:8889
# 查看代理设置
npm config ls -l | grep proxy
```

**用 npm 安装 yarn**

```bash
npm install yarn -g
```

