---
layout: post
title: 基础
categories: Znote
description: 面试基础
keywords: 基础, 面试
---

> Java基础

1. &和&&的区别
    &和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true时，整个运算结果才为true，否则，只要有一方为false，则结果为false。&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式，例如，对于if(str != null && !str.equals(“”))表达式，当str为null时，后面的表达式不会执行，所以不会出现NullPointerException如果将&&改为&，则会抛出NullPointerException异常。If(x==33 & ++y>0) y会增长，If(x==33 && ++y>0)不会增长。

    &还可以用作位运算符，当&操作符两边的表达式不是boolean类型时，&表示按位与操作，我们通常使用0x0f来与一个整数进行&运算，来获取该整数的最低4个bit位，例如，0x31 & 0x0f的结果为0x01。

    *备注：这道题先说两者的共同点，再说出&&和&的特殊之处，并列举一些经典的例子来表明自己理解透彻深入、实际经验丰富。* 

2. switch语句能否作用在byte上，能否作用在long上，能否作用在String上?

   ​

3. 接口是否可继承接口? 抽象类是否可实现(implements)接口? 抽象类是否可继承具体类(concrete class)? 抽象类中是否可以有静态的main方法？

   接口可以继承接口。抽象类可以实现(implements)接口，抽象类可继承具体类。抽象类中可以有静态的main方法。

   *备注：只要明白了接口和抽象类的本质和作用，这些问题都很好回答，你想想，如果你是java语言的设计者，你是否会提供这样的支持，如果不提供的话，有什么理由吗？如果你没有道理不提供，那答案就是肯定的了。只有记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。* 

4. String和StringBuffer区别

   String是不可变的（final），每次改变都相当于创建一个对象，耗费性能，GC回收会变的很慢

   StringBuffer长度是可变的，效率比String高，每次增加长度是16，而且是线程安全的，StringBuilder是线程非安全的，但效率比StringBuffer高。

5. 请写出你最常见到的5个runtimeexception

    NullPointerException - 空指针引用异常
    ClassCastException - 类型强制转换异常。
    IllegalArgumentException - 传递非法参数异常。
    ArithmeticException - 算术运算异常
    ArrayStoreException - 向数组中存放与声明类型不兼容对象异常
    IndexOutOfBoundsException - 下标越界异常
    NegativeArraySizeException - 创建一个大小为负数的数组错误异常
    NumberFormatException - 数字格式异常
    SecurityException - 安全异常
    UnsupportedOperationException - 不支持的操作异常

    ​

    异常处理
    switch

4. 数据库
  乐观锁和悲观锁

5. jvm