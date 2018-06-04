---
layout: post
title:  "IDEA 生成JPA实体"
date:   2018-05-22 10:14:00 +0800
categories: idea jpa
tags: jpa 
---

## 添加JPA支持

在`file->project structure->modules`中，点击绿色加号，添加JPA

## 调出Persistence窗口

双击alt，在左下角点击persistence

## 生成

1. 右键entityFactory->generate persistence mapping
2. 选择数据源
3. 设置包名
4. 选择要生成的表
5. 选中Generate JPA Annotations
6. 点击ok进行生成
