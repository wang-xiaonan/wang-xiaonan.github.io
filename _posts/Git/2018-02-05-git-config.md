---
layout: post
title: Git 配置
categories: Git
description: Git config
keywords: 配置, git
---

> Git 配置基本参数

#### 查看配置

```
git config --global --list
或具体某个参数
git config --global http.proxy
git config --global https.proxy
```
#### 设置用户名和邮箱

> - 用户名：`git config --global user.name yourname`
> - 邮件：`git config --global user.email youremailadrss` 

#### 设置代理

```
git config --global http.proxy http://proxyhost:port
git config --global https.proxy https://proxyhost:port
或（带用户密码）
git config --global http.proxy http://user:password@proxyhost:port
git config --global https.proxy https://user:password@proxyhost:port
```
#### 删除设置

```
git config --global --unset http.proxy
git config --global --unset user.name
```