---
layout: post
title:  "Thymeleaf无法解析`sec:***`标签"
date:   2018-04-28 3:36:40 +0800
categories: web
tags: spring thymeleaf sec
---

在用Thymeleaf时发现`sec:authorize="hasRole('ROOT')"`标签不能被解析，在pom中添加如下依赖即可:

```xml
<dependency>
    <groupId>org.thymeleaf.extras</groupId>
    <artifactId>thymeleaf-extras-springsecurity4</artifactId>
    <version>3.0.2.RELEASE</version>
</dependency>
```



Env:
springboot2
spring security5
