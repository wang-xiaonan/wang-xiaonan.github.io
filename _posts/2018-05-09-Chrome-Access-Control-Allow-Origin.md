---
layout: post
title: Chrome 解决跨域调用问题
categories: Znote
description: Chrome 本地调试跨域问题解决
keywords: chrome, 跨域
---

> Chrome 浏览器本地调试屏蔽跨域调用检查

找到 Chrome 浏览器快捷方式 ==》属性 ==》快捷方式 ==》目标 ==》在引号后面追加 `--args --disable-web-security --user-data-dir` （注意`--args`前面有个空格）

点击快捷方式打开 Chrome 就会提示“您使用的是不受支持的命令行标记：--disable-web-security。稳定性和安全性会有所下降。”表示更改已经成功。