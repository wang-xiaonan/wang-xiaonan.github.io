---
layout: post
title: Spring Boot NoClassDefFoundError
categories: Spring
description: NoClassDefFoundError
keywords: spring boot, noclass, error
---

> java.lang.NoClassDefFoundError: org/springframework/boot/SpringBootConfiguration

Spring Boot 新建项目启动报错，试了网上的很多的办法，没有效果，最后到本地的 `repository（D:\.m2\repository\org\springframework\boot\spring-boot）`下，把下面的所有的文件删除掉；  

然后maven clean >> 运行项目成功！