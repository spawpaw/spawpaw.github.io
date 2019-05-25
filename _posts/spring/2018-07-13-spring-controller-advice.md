---
layout: post
title:  "spring-boot-2.0 中的jackson不将时间转换成时间戳的问题"
date:   2018-05-14 13:50:40 +0800
categories: spring
tags: springboot date-format
---


项目中使用了SpringBoot，需要的得时间类型为long型时间戳，但是2.0默认解析出来的时间为字符串，只要在配置文件中加上：

```yaml
spring:
  jackson:
    serialization.write-dates-as-timestamps: true
```

就可以强制将时间解析成时间戳