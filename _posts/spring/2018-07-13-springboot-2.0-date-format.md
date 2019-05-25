---
layout: post
title:  "spring-boot-devtools在Idea中热部署方法"
date:   2018-05-14 13:50:40 +0800
categories: spring
tags: springboot devtools
---

### 1 pom.xml文件

注：热部署功能spring-boot-1.3开始有的

```xml
<!--添加依赖-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <!-- optional=true,依赖不会传递，该项目依赖devtools；之后依赖myboot项目的项目如果想要使用devtools，需要重新引入 -->
    <optional>true</optional>
</dependency>
```

注：project 中添加 spring-boot-maven-plugin,主要在eclipse中使用，idea中不需要添加此配置。

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>
            </configuration>
        </plugin>
    </plugins>
</build>
```

### 2 更改idea配置

　　1） “File” -> “Settings” -> “Build,Execution,Deplyment” -> “Compiler”，选中打勾 “Build project automatically” 。

　　2） 组合键：“Shift+Ctrl+Alt+/” ，选择 “Registry” ，选中打勾 “compiler.automake.allow.when.app.running” 。

### 3 Chrome禁用缓存

　　F12或者“Ctrl+Shift+I”，打开开发者工具，“Network” 选项卡下 选中打勾 “Disable Cache(while DevTools is open)” 