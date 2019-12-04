---
title: java环境变量配置
date: 2019-08-10 20:17:12
categories:
  - technology
  - back-end
tags:
  - config
  - java
---
# window10下环境变量配置

## 新建JAVA_HOME

变量名：JAVA_HOME
变量值：电脑上JDK安装的绝对路径

## 新建/修改 CLASSPATH 变量

变量名：CLASSPATH
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

## 修改Path 变量

新建两条路径：

%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin


参考文档
https://www.runoob.com/w3cnote/windows10-java-setup.html