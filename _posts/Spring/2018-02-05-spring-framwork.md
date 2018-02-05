---
layout: post
title: Spring 框架结构
categories: Spring
description: Spring Framework
keywords: Spring, Spring Framework
---

### Spring Framework 

> Spring Framework包含了大约20个模块，被分成一下Core Container, Data Access/Integration, Web, AOP (Aspect Oriented Programming), Instrumentation, Messaging和Test这6个部分，每个模块都有一个jar包，instrumentation模块有两个jar，图中还缺少spring-context-support模块。

![spring-overview](/images/spring/spring-overview.png)
1. Core Container
  核心部分包含：spring-core，spring-beans，spring-context，spring-context-support，spring-expression (Spring Expression Language) 模块。
    - spring-core：Spring框架基本的核心工具类，提供了IoC和DI最基本实现
    - spring-beans：Bean工厂与bean的装配，配置文件访问等
    - spring-context：spring的context上下文即IoC容器
    - spring-expression：spring表达式支持
        [表达式语言 Spring Expression Language](http://www.cnblogs.com/best/p/5748105.html)
    - spring-context-support：spring额外支持包，如邮件服务、视图解析等

    依赖关系：可以在maven仓库查询依赖关系http://mvnrepository.com
  ![Core Container](/images/spring/Core-Container.png)

2. AOP and Instrumentation
  模块包含：spring-aop，spring-aspects，spring-instrument，spring-instrument-tomcat
    - spring-aop：面向切面编程
    - spring-aspects：集成AspectJ
    - spring-instrument：向服务器提供类级的工具支持和classloader的实现
    - spring-instrument-tomcat：针对tomcat的instrument实现

    依赖关系：[Spring Aspects](http://mvnrepository.com/artifact/org.springframework/spring-aspects/4.3.0.RELEASE)，[spring-aop](http://mvnrepository.com/artifact/org.springframework/spring-aop/4.3.0.RELEASE)


3. Messaging
  模块包含：spring-messaging
  从spring4开始的模块
    - spring-messaging：用于构建基于消息的应用程序
       依赖关系： [Spring Messaging](http://mvnrepository.com/artifact/org.springframework/spring-messaging)

4. Data Access/Integration
  模块包含：spring-jdbc，spring-tx，spring-orm，spring-oxm，spring-jms，spring-messaging
    - spring-jdbc：jdbc支持
    - spring-tx：事务控制
    - spring-orm：对象关系映射API，集成JPA，JDO，Hibernate等orm框架
    - spring-oxm：对象XML映射
    - spring-jms：java消息服务，从spring4.1开始jms集成了spring-messaging

5. Web
  模块包含：spring-web，spring-webmvc，spring-websocket，spring-webmvc-portlet
    - spring-web：基础的web功能，包括文件上传等
    - spring-webmvc：mvc实现
    - spring-websocket：spring4开始，为web应用提供的高效通信工具
    - spring-webmvc-portlet：基于portlet的mvc实现

6. Test
  模块包含：spring-test
    - spring-test：spring测试，提供junit与mock测试功能

使用spring
> spring所有的groupId都是`org.springframework`，只是artifactId不同

根据spring的依赖关系，普通的java工程中需要引用一个dependency
```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>xxxxxxxxx</version>
</dependency>
```
如果是web工程只需配置
```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>xxxxxxxxx</version>
</dependency>
```
### 参考

[Spring Framework Reference Documentation](https://docs.spring.io/spring/docs/4.3.14.BUILD-SNAPSHOT/spring-framework-reference/htmlsingle/#overview-data-access) 