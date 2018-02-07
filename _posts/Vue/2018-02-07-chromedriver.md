---
layout: post
title: vue-cli搭建环境时报错
categories: Vue
description: vue-cli搭建环境时报错
keywords: vue-cli
---

> vue-cli脚手架搭建环境时报 Failed at the chromedriver@2.33.1 install script.

错误：
```
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! chromedriver@2.33.1 install: `node install.js`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the chromedriver@2.33.1 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.
```

解决办法:

 `npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver`