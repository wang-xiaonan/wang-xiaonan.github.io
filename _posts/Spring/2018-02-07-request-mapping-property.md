---
layout: post
title: @RequestMapping Property
categories: Spring
description: RequestMapping 注解属性
keywords: RequestMapping, Property
---

@RequestMapping注解六个属性

### 1、 value， method；

value：     指定请求的实际地址，指定的地址可以是URI Template 模式；

method：  指定请求的method类型， GET、POST、PUT、DELETE等；

### 2、 consumes，produces；

consumes： 指定处理请求的提交内容类型（Content-Type），例如application/json, text/html;

produces:    指定返回的内容类型，仅当request请求头中的(Accept)类型中包含该指定类型才返回；

### 3、 params，headers；

params： 指定request中必须包含某些参数值是，才让该方法处理。

headers： 指定request中必须包含某些指定的header值，才能让该方法处理请求。