---
layout: post
title: "Lombok-安装"
date:   2018-07-15 11:23:00 +0800
categories: java
tags: lombok
---

##  Installation
### 插件安装
- 使用IDEA自带的插件管理器安装(Windows)：
  - `File` > `Settings` > `Plugins` > `Browse repositories...` > `Search for "lombok"` > `Install Plugin`
- 使用IDEA自带的插件管理器安装(MacOs)：
  - `Preferences` > `Settings` > `Plugins` > `Browse repositories...` > `Search for "lombok"` > `Install Plugin`
- 手动安装:
  - 下载 [最新版本插件](https://github.com/mplushnikov/lombok-intellij-plugin/releases/tag/releasebuild_0.19) 并通过如下方式安装： `Preferences` > `Plugins` >` Install plugin from disk...`  

重启 IDE.

### IntelliJ 配置
在项目中: `单击 Preferences` -> `Build, Execution, Deployment` -> `Compiler, Annotation Processors`. 单击 `Enable Annotation Processing`

之后你需要通过 `Build` -> `Rebuild Project`来重新构建你的项目

### 为项目添加 Lombok 依赖
确保你的项目中已经添加了Lombok依赖，因为插件并不会自动帮你添加

提示: 推荐使用最新版本的Lombok依赖，但并不保证所有功能

如果你使用 Gradle/Maven/Ivy 作为项目管理工具，参见如下例子：

#### Gradle
在 `build.gradle` 中:

```groovy
// 'compile' can be changed to 'compileOnly' for Gradle 2.12+
// or 'provided' if using 'propdeps' plugin from SpringSource
compile "org.projectlombok:lombok:1.18.0"
```

#### Maven
在 `pom.xml` 中:
```xml
<dependencies>
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>1.18.0</version>
		<scope>provided</scope>
	</dependency>
</dependencies>
```

#### Ivy
在 `ivy.xml` 中:
```xml
<dependency org="org.projectlombok" name="lombok" rev="1.18.0" conf="build" />
```


> [lombok-intellij-plugin](https://github.com/mplushnikov/lombok-intellij-plugin)  
> [Lombok on Maven](http://mvnrepository.com/artifact/org.projectlombok/lombok)