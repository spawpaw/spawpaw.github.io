---
layout: post
title: "Java 运行时数据区"
date:   2018-07-15 11:23:00 +0800
categories: java
tags: lomblok
---

在[The Java Virtual Machine Specification : Java SE 7 ](https://docs.oracle.com/javase/specs/jvms/se7/jvms7.pdf)的第2.5节中介绍了JVM运行时数据区

![/img/jvm-runtime-data-area.png](https://github.com/spawpaw/spawpaw.github.io/blob/master/img/jvm-runtime-data-area.png?raw=true)

### 程序计数器 ( PC Register )

PC是一块较小的内存空间，在JVM的概念模型里，字节码解释器工作时就是通过这个计数器的值来获取下一条需要执行的字节码指令。  
每个线程都有一个独立的程序计数器，用于在线程切换后能够恢复到正确的执行位置。  
如果正在执行的是一个Java方法，这个计数器记录的是正在执行的虚拟机字节码指令的地址。  
如果正在执行的是一个Native方法，这个计数器的值为空（Undefined）

这个内存区域是JVM中唯一没有规定任何OutOfMemory情况的区域。  

### Java虚拟机栈 (Stack)

和PC一样，JVM Stacks也是线程私有的。
每个方法在执行的同时都会创建一个栈帧（Stack Frame）用于存储`局部变量表`、`操作数栈`、`动态链接`、`方法出口`等信息。每一个方法从调用到执行完毕的过程，都对应者一个栈帧从入栈到出栈的过程。
局部变量表存放了编译器可以预知的各种基本数据类型（boolean,byte,char,short,int,float,long,double）、对象引用(reference)和returnAddress类型。其中64为的long和double类型会占用2个局部变量空间（Slot），其余的数据类型只会占用1个。
局部变量表所需的内存空间在编译期间完成分配，在运行期间不会改变局部变量表的大小。


在JVM规范中，对该区域规定了两种异常情况：
- StackOverFlowException: 线程请求的栈深度大于虚拟机所允许的深度
- OutOfMemoryError: 如果虚拟机栈支持动态扩展（大部分虚拟机都可以动态扩展），且扩展时无法申请到足够的内存

### Native Method Stack本地方法栈

和虚拟机方法栈发挥的作用类似，本地方法栈为虚拟机所使用的Native方法服务。有的虚拟机直接把本地方法栈和虚拟机栈合二为一(Sun HotSpot虚拟机)。


### Heap 堆
Java堆是JVM所管理的内存中最大的一块，所有线程共享，在虚拟机启动时创建。
所有对象实例都在这里分配内存，但随着JIT编译器的发展与`逃逸分析`技术逐渐成熟，`栈上分配`、`标量替换`优化技术会导致一些微妙变化的发生。





> 逃逸分析:  
> 栈上分配:  
> 标量替换:  

### Method Area方法区

方法区是被所有线程共享，所有字段和方法字节码，以及一些特殊方法如构造函数，接口代码也在此定义。简单说，所有定义的方法的信息都保存在该区域，此区域属于共享区间。
静态变量+常量+类信息+运行时常量池存在方法区中，实例变量存在堆内存中。

#### 运行时常量池（Runtime Constant Pool）（NIO）

运行时常量池时方法区的一部分。用于存放编译期生成的各种字面量和符号引用


### 直接内存（DirectMemory）
直接内存并不是JVM运行时数据区的一部分，也不是JVM规范定义的内存区域。