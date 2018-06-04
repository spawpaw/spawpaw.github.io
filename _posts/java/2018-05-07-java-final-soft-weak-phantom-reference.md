---
layout: post
title:  "Java对象的强、软、弱、虚引用"
date:   2018-05-07 09:39:00 +0800
categories: java
tags: 
---
### 对象图

- java.lang.Object
    - java.lang.ref.ReferenceQueue
    - java.lang.ref.Reference
        - java.lang.ref.FinalReference      强引用
        - java.lang.ref.SoftReference       软引用
        - java.lang.ref.WeakReference       弱引用
        - java.lang.ref.PhantomReference    虚引用

### 强引用
如果一个对象有强引用，那么垃圾回收器绝对不会回收它

|引用类型|GC回收时间|用途|生存时间|
|:---:|:---:|:---:|:---:|
|强引用|never     |对象的一般状态|JVM停止运行|
|软引用|内存不足时 |对象缓存     |内存不足时 |
|弱引用|GC时      |对象缓存     |GC后       |
|虚引用|unknown   |unknown     |unknown    |