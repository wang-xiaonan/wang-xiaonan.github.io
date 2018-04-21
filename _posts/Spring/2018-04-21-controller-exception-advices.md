---
layout: post
title: ControllerAdvices
categories: Spring
description: Controller advices
keywords: exception, advices
---

> Controller 层异常处理

最近看见项目中在 Controller 层抛出了异常，如果访问过程出现错误，前端页面就会出现非常不友好的提示，一般的设计原则不是应该尽量在 Service 层中抛出异常，在 Controller 层中捕获并返回客户端数据？

下面记录一下，在 Controller 层统一处理异常的方式：

1. Controller 层并不需要做什么操作，抛出异常就好了

2. 创建异常捕获类，并标注 @ControllerAdvice，并注入到 Spring 容器中

   ```java
   @ControllerAdvice
   @Component
   public class ControllerAdvices {

       @ResponseBody
       @ExceptionHandler(RuntimeException.class)
       public String runtimeException(RuntimeException e){
           System.out.println(e.getMessage());
           return "RuntimeExceptinn: 异常捕获";
       }

       @ResponseBody
       // 如果 ExceptionHandler 注解中未声明异常类型，默认为参数列表中的异常
       @ExceptionHandler(WrapperException.class)
       public String otherException(WrapperException e){
           System.out.println(e.getMessage());
           return "WrapperException: 异常捕获";
       }
   }
   ```
   自定义的异常类
   ```java
   public class WrapperException extends RuntimeException {
       public WrapperException() {
           super();
       }

       public WrapperException(String message) {
           super(message);
       }
   }
   ```

   ​