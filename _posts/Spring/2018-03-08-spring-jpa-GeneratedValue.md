---
layout: post
title: JPA @GeneratedValue
categories: Spring
description: JPA 之 @GeneratedValue
keywords: GeneratedValue, JPA
---

> @GeneratedValue 主键策略

JPA 要求每一个 Entity 必须有且只有一个主键，通过注解的形式映射Hibernate实体，主键用@Id标识，其生成规则用@GeneratedValue表示。

@GeneratedValue 有两个属性，strategy 和 generator 。generator  默认为""，是用来声明主键生成器的名称， 供@SequenceGenerator 和 @TableGenerator 的 name 属性使用，和 @GeneratedValue 进行关联。

@GeneratedValue 有四种主键生成策略，TABLE, SEQUENCE, IDENTITY, AUTO

#### GenerationType.TABLE

使用一个特殊的数据库表保存主键，持久化引擎通数据库表生成主键，优点：不依赖于外部环境和数据库的具体实现，可以在不同数据库很容易移植。缺点：不能很好的利用数据库的特性，一般不推荐优先使用。

该策略配合 @TableGenerator 注解使用，name 属性填写 @GeneratedValue 的 generator 值；table 属性填写用来持久化主键所使用的数据库表；pkColumnName 属性填写数据库表中保存主键的列名；valueColumnName 属性填写保存主键值的列名；initialValue 属性填写初始化值；allocationSize 属性填写主键生成的增量；

```java
@Id  
@GeneratedValue(strategy = GenerationType.TABLE, generator = "g_id")  
@TableGenerator(name = "g_id", table = "t_id_table", pkColumnName = "table_name",  valueColumnName = "id_num", initialValue = 0, allocationSize = 1)  
private Integer id; 
```

#### GenerationType.SEQUENCE

在链接 Oracle 等部分提供序列机制生成主键数据库时提供的主键自增策略，优点和缺点正好和 GenerationType.TABLE 策略相反。该策略配合 @SequenceGenerator 使用

```java
@Id  
@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "menuSeq")  
@SequenceGenerator(name = "menuSeq", initialValue = 1, allocationSize = 1, sequenceName = "MENU_SEQUENCE")  
private Integer id; 
```

sequenceName 属性填写 Oracle 等数据库创建的主键自增设置的序列名

#### GenerationType.IDENTITY

此种主键生成策略就是通常所说的主键自增长,数据库在插入数据时,会自动给主键赋值,比如 MYSQL 可以在创建表时声明 auto_increment 来指定主键自增长。该策略在大部分数据库中都提供了支持(指定方法或关键字可能不同),但还是有少数数据库不支持,所以可移植性略差。使用自增长主键生成策略是只需要声明 strategy = GenerationType.IDENTITY ，注意同一张表中自增列最多有一列。

```java
@Id
@GenerateValue(strategy = GenerationType.IDENTITY)
private Integer id;
```

#### GenerationType.AUTO

此策略会把主键生成交给持久化引擎（persistence engine），持久化引擎会从以上三种策略中选择一种，此主键生成策略比较常用。此策略时 JPA 默认使用的，所以在使用时可以显示指定，也可以只写 @GeneratedValue 。

```java
@Id
@GeneratedValue
private Integer id;
```

```java
@Id
@GeneratedValue(strategy = GenerationType.AUTO)
private Integer id;
```

参考：

 [JPA 批注参考](http://www.oracle.com/technetwork/cn/middleware/ias/toplink-jpa-annotations-100895-zhs.html#) 

 [Java 持久化技术规范（JPA）中的主键生成策略](https://www.ibm.com/developerworks/cn/java/j-lo-jpaprimarykey/) 