---
layout: post
title:  "spring对接口响应体进行统一的封装"
date:   2018-07-13 21:50:00 +0800
categories: spring
tags: spring-boot date-format
---


## 需求分析

## 现在的接口
在日常的开发中通常会遇到对同一个接口进行访问的时候，成功响应体和异常响应体不一致的情况。
例如成功创建一个用户时的响应体为：
```json
{
    "id": 10000,
    "username": "123456",
    "password": "test",
    "avatar": "http://cdn.appx.host/avatar/10000",
    "createTime": 1515000000000
}
```

失败时的响应体为（spring默认的响应体格式）：
```json
{
    "status": 400,
    "error": "Bad Request",
    "message": "参数无效",
    "path": "/api/user",
    "exception": "org.springframework.web.bind.MethodArgumentNotValidException",
    "errors": [
        {
            "fieldName": "id",
            "message": "invalid"
        }
    ],
    "timestamp": 1515000000000
}
```

目前很多平台的API都为上面的格式，比如`github api(v3)`, 这样做的缺点就是要通过读取HTTP的头部来判断响应状态，在某些情况下有些不便。


## 期望的接口

对响应体进行统一的封装，目前主流的做法分为两种，一种是将附加的信息写在HTTP头中，比如github的api(v3)，将分页的数据写在另一种是构造一个基类来存储附加信息，而


## 实现思路
### 确定响应体的格式
### 对成功时的响应体进行封装

### 对失败时的响应体进行封装
在对失败响应体进行封装之前，我们首先要处理几个问题：

- 错误码放在哪里
- 自定义异常
- 非自定义异常到错误码的映射

## 代码实现