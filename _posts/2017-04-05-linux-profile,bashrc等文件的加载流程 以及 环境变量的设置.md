---
layout: post
title:  "linux /etc/profile,bashrc等文件的加载流程 以及 环境变量的设置"
date:   2017-04-05 16:45:40 +0800
categories: linux
tags: 环境变量 profile bashrc
---

>因为最近在debian上设置java环境变量，研究了一下profile等文件的加载流程
其实在ubuntu上也很相似，其他发行版的linux没有研究过。

环境变量一般在profile文件中设置，

- 如果只想本次登陆shell有效，直接在shell中输入 `export 变量名=变量值1[:变量值2[:...]]`  
- 如果只想对当前用户生效，就在`~/.profile` 中设置，
- 如果想让设置对所有用户生效，就在`etc/profile` 中设置。

设置的方法很简单，只要在文件末尾按照如下语法添加
```bash
export 变量名=变量值1[:变量值2[:...]]
```

例如为所有用户添加java环境变量(注意，多个变量之间是**用冒号**分隔，而**不是分号**)：
```bash
#在/etc/profile 的末尾追加如下内容，JAVA_HOME改成你自己java的目录
export JAVA_HOME=/usr/share/jdk1.8
export PATH=$JAVA_HOME/bin:$PATH 
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar 
```


各个文件的加载顺序(其实系统启动时只加载了profile文件，然后profile文件递归加载了其余的文件)：

￼￼![linux /etc/profile,bashrc等文件的 加载流程](http://img.blog.csdn.net/20170405223231326?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjk3NTMyODU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
