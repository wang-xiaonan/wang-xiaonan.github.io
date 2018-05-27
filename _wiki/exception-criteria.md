---
layout: wiki
title: 日志约定
categories: Logger
description: using standards
keywords: logger, criteria
---

> 日志打印规范，参考总结

![](/images/wiki/concrete-bindings.png)

#### 日志级别

Custom Log Levels

| Log Levels |                                                  | intLevel          |
| ---------- | ------------------------------------------------ | ----------------- |
| OFF        |                                                  | 0                 |
| FATAL      | 严重的错误事件将会导致应用程序的退出             | 100               |
| ERROR      | 指出虽然发生错误事件，但仍然不影响系统的继续运行 | 200               |
| WARN       | 表明会出现潜在错误的情形                         | 300               |
| INFO       | 消息在粗粒度级别上突出强调应用程序的运行过程     | 400               |
| DEBUG      | 指出细粒度信息事件对调试应用程序                 | 500               |
| TRACE      | 更详细的跟踪信息                                 | 600               |
| ALL        |                                                  | Integer.MAX_VALUE |

级别之间是包含关系， （FATAL > ERROR > WARN > INFO > DEBUG > TRACE）FATAL级别最高，级别越小intLevel值越大，包含的信息越多（TRACE=600，包含 0 ~ 600 之间的所有日志级别）。

1. FATAL，ERROR：系统发生了严重的错误，必须由人员进行检查和处理
2. WARN：业务可以继续向下进行，但可能存在潜在的问题，必须引起运维人员的注意，并进行检查
3. INFO：可以是业务一个阶段处理完成进行记录，有助于通过 info 判断问题出在什么阶段，很快的定位错误地点
4. DEBUG，TRACE：用于开发人员，从不同粒度记录业务流程进行的状况，便于开发和测试

#### Logger 使用约定

1. 一个对象使用一个 Logger 对象，一般是 `private static final` ，在少数情况必要的情况下才使用 `ptivate final` 

   ```java
   private static final Logger logger = LoggerFactory.getLogger(xxx.class);
   ```

2. 最重要的一定要确保不会因为 logger 语句抛出异常情况

   ```java
   logger.info("some info : {}", object.getInfo());
   ```

   可能无法确保 object 是否为 null，会造成抛出异常。

3. 避免使用字符串拼接的形式

   ```java
   logger.info("userName=" + userName + ", phoneNo=" + phoneNo);
   logger.info("userName={}, phoneNo={}"， userName， phoneNo);// 推荐
   ```
   如果日志输出的频率非常高，再使用字符串拼接的形式会造成程序性能的下降，使用 Slf4j 提供的第二种方式简单方便。

4. 代码方法入参，业务流程结果等，如果要记录日志或者想记录日志，可以使用 DEBUG 级别的

   ```java
   logger.debug("[saveUserInfo]:{}", userInfo);
   ```

   平时开发时区分出 info 和 debug 打印的信息，避免所有日志都打印到一个文件中，造成日志分析工作非常困难。

5. ERROR 级别以上的信息输出 Exception 全部的 Throwable 信息

   ```java
   try {
       // something ...
   } catch (Exception e) {
       logger.error(e.getMessage());
       logger.error("error", e.getMessage());
       logger.error("error", e);// 推荐
   }
   ```

6. 尽量避免记录日志又抛出异常

   ```java
   try {
       // something ...
   } catch (Exception e) {
       logger.error("error", e);
       throw new ServiceException("something wrong");
   }
   ```

   会造成错误信息多次记录的问题，原则上只允许记录一次日志信息。

   *在实际开发中，如果是向外提供接口，个人认为在最外层接口处，应该允许记录日志同时抛出异常，或者是记录日志同时返回错误信息（不抛出异常）* 

7. 不允许使用 System.out 或者 System.error 输出日志信息，或者 printStackTrace

   ```java
   try {
       // do something ...
   } catch （Exception e）{
       System.out.print(e.getMessage());// 不允许
       System.out.print(e.getMessage());// 不允许
       e.printStackTrace();// 不允许
   }
   ```

8. 输出一些有意义的信息，`easy to read, easy to parse ` 

   ```java
   try {
       // do something ...
   } catch （Exception e）{
       logger.debug("error");// 不推荐
       logger.debug("something is wrong : param = {}", param);// 推荐
   }
   ```

   推荐日志要有意义，易懂，同时尽量不要包含个人隐私信息，银行卡，身份证等信息。

#### 总结

现在比较流行的，公司目前使用的是 Slf4j + logback 这种组合形式

参考：

https://www.slf4j.org/index.html

https://logback.qos.ch/

https://logging.apache.org/log4j/2.x/

https://www.jianshu.com/p/8551fe9c6354

[What is the fastest way of (not) logging?](https://www.slf4j.org/faq.html#logging_performance)  