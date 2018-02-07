---
layout: post
title: npm 配置
categories: Node
description: npm 环境配置
keywords: npm, 配置
---

> npm 环境配置

npm config set <key> <value> [-g|--global]

#### 设置代理

```
npm config set proxy http://username:password@ip:port
npm config delete proxy
```

#### 设置镜像地址

```
npm config set registry http://registry.npmjs.org
```

[淘宝镜像](https://npm.taobao.org/)：https://registry.npm.taobao.org/

#### 设置缓存路径

```
npm config set cache "D:\nodejs\node_cache"
```

#### 设置全局目录

```
npm config set prefix "D:\nodejs\node_global"
```

#### 参考

- [npm 中文文档](https://www.npmjs.com.cn/)