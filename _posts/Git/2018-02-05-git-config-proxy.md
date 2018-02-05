---
layout: post
title: Git 设置代理
categories: Git
description: 设置 Git 代理
keywords: 代理, http.proxy，设置代理
---

### Git 设置 Http 代理

#### 查看代理

```
git config --global --list
或
git config --global http.proxy
git config --global https.proxy
```
#### 设置代理

```
git config --global http.proxy http://proxyhost:port
git config --global https.proxy https://proxyhost:port
或（带用户密码）
git config --global http.proxy http://user:password@proxyhost:port
git config --global https.proxy https://user:password@proxyhost:port
```
#### 取消代理

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```