---
layout: post
title: Redis（Windows）安装
categories: Redis
description: redis install
keywords: redis
---

> Redis 在 Windows 环境下安装过程



#### 下载 Windows 版 Redis

官网下载：https://redis.io/download （我没打开）

MS 维护的 GitHub地址： https://github.com/MicrosoftArchive/redis/releases 

#### 安装 Redis

1. 将下载的 Redis 解压，cmd 到该目录
2. 启动，redis-server redis.windows.conf
3. 测试，redis-cli -h 127.0.0.1 -p 6379

#### 将 Redis 添加到 Windows 服务

- installing the service

  redis-server --service-install redis.windows-service.conf --loglevel verbose

- uninstalling the service

  redis-server --service-uninstall

- starting the service

  redis-server --service-start

- stopping the service

  redis-server --service-stop

- naming the service

  redis-server --service-install --service-nameredisService1 --port 10001

  redis-server --service-start --service-name redisService1

  redis-server --service-install --service-nameredisService2 --port 10002

  redis-server --service-start --service-name redisService2