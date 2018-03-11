---
title: Android Build System 之 理解Gradle, Android Plugin for Gradle
layout:  post  
categories: Android
description: 理解Gradle, Android Plugin for Gradle  
---

### 参考  
https://developer.android.com/studio/releases/gradle-plugin.html#updating-plugin  
https://developer.android.com/studio/build/index.html

### 简介Gradle  
Gradle 是一套先进的构建工具。Android studio 使用Gradle，来自动执行和管理每次的构建，你可以方便的自定义配置。每一个构建配置可以定义单独的一套源码和资源，同时对相同资源进行复用。
Android plugin for Gradle 与Gradle配合工作， 定义一系列操作和配置选项。

### 理解  
Gradle 是构建工具，用来执行，比如编译，打包，签名，发布等等。build.gradle 是我们定义的构建规则，需要我们自己去定义。手写比较繁琐，所以前辈们已经帮我们写好了， 就是这些plugin。plugin 是规则，是构建逻辑。Gradle根据这一系列规则去执行。
Gradle 相当于make， Plugin相当于makefile。  

### 版本
Gradle 和 Android Plug for Gradle都有各自的版本号，都是独立升级的。但是这两者的版本需要匹配，否则会出现兼容问题。  
为了更好的性能体验，建议Gradle和Android Plugin这两者都更新到最新版本。两者匹配关系如下(截至20171012)

Plugin version|	Required Gradle version
--|--
1.0.0 - 1.1.3	|2.2.1 - 2.3
1.2.0 - 1.3.1	|2.2.1 - 2.9
1.5.0	|2.2.1 - 2.13
2.0.0 - 2.1.2	|2.10 - 2.13
2.1.3 - 2.2.3	|2.14.1+
2.3.0+	|3.3+

### 更多  
对于Gradle而言，不仅可以构建android项目，其他项目也可以构建，只要写好plugin 就可以了。例如，编译android系统用 android plugin， 编译java程序有java plugin，等等。
