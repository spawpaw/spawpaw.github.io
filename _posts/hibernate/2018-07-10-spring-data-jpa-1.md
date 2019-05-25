---
layout: post
title:  "Spring Data JPA入门"
date:   2018-05-14 13:50:40 +0800
categories: spring
tags: spring-data-jpa hibernate
---
## 简介

### `Spring Data JPA`是什么
Spring Data 是Spring 的一个子项目， 旨在统一和简化对各类型持久化存储， 而不拘泥于是关系型数据库还是NoSQL 数据存储。
`Spring Data JPA`为`Java Persistence API（JPA）`提供了存储库支持。它简化了需要访问JPA数据源的应用程序的开发。

无论是哪种持久化存储， 数据访问对象（或称作为DAO，即Data Access Objects）通常都会提供对单一域对象的CRUD （创建、读取、更新、删除）操作、查询方法、排序和分页方法等。
Spring Data则提供了基于这些层面的统一接口（`CrudRepository`，`PagingAndSortingRepository`）以及对持久化存储的实现。

Spring Data JPA 框架，主要针对的就是 Spring 唯一没有简化到的业务逻辑代码，至此，开发者连仅剩的实现持久层业务逻辑的工作都省了，唯一要做的，就只是声明持久层的接口，其他都交给 Spring Data JPA 来帮你完成！

Spring data jpa是在JPA规范下提供了Repository层的实现，但是使用哪一种ORM需要你来决定（默认使用Hibernate JPA的实现）。虽然ORM框架都实现了JPA规范，但是在不同的ORM框架之间切换仍然需要编写不同的代码，而通过使用Spring data jpa能够方便大家在不同的ORM框架之间进行切换而不要更改代码。并且spring data jpa 对Repository层封装的很好，也省去了不少的麻烦。 


### 什么是JPA

JPA java persistence api ,为POJO(就是我们的JavaBean)提供持久化标准规范，JavaEE规范之一。

主要思想,3个：

- `ORM映射、实体持久化`：ORM(Object Relational Mapping)映射元数据，通过XML或注解，描述对象和表之间的关系，框架据此将实体对象持久化到数据库
- `实体对象、JDBC和SQL、解脱`：规范的API，通过操作实体对象，就能执行对应数据库的CRUD操作，ORM框架让开发从繁琐的JDBC和SQL代码中解脱出来
- `面向对象查询、SQL解耦`：查询语言，通过面向对象而非面向数据库的查询语言查询数据，避免程序的SQL语句紧密耦合

简而言之就是规范了实体如何定义，实体之间有哪些关系

## 依赖


可在[https://github.com/spring-projects/spring-data-jpa](https://github.com/spring-projects/spring-data-jpa)查看`Spring Data JPA`的所有版本。目前的最新版本为[![Spring Data JPA](https://spring.io/badges/spring-data-jpa/ga.svg)](http://projects.spring.io/spring-data-jpa/#quick-start)，直接在下面的xml中将版本号替换即可。

### maven依赖

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-jpa</artifactId>
    <version>2.0.8.RELEASE</version>
</dependency>
```

如果使用了SpringBoot，则使用如下依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```


## 参考文档
> [Spring Data JPA 官方文档](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)