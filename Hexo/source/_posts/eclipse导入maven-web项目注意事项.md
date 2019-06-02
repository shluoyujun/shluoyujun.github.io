---
title: eclipse导入maven web项目注意事项
date: 2017-04-29 15:02:06
categories:
	 - environment
tags: [web,eclipse,java]
---
eclipse导入已经存在的maven web项目还需要进行一些简单的配置，这里记录一下可能遇到的情况。

导入方法：
File -> Import -> Maven -> Existing Maven Projects

导入过程可能的报错及解决方法
<!-- more --> 
1 pom.xml
报错：Plugin execution not covered by lifecycle configuration
解决方法：在
```
<build>和<plugins>
```
之间加入
```
<pluginManagement>
```
如果build出错，在
```
<build></build>
```
之间找个地方加入
```
<defaultGoal>compile</defaultGoal>
```

2 环境问题
出现的错误如下
![](http://i4.buimg.com/4851/5aa0b41fc757410e.png)
解决方法：
(1) Properties -> Java Build Path 
	修改JRE版本为1.8
(2) Properties ->JavaCompiler  
	看一下Compiler compliance level 的版本是否为1.8，如果不是修改为1.8
(3) Properties -> Project Facets
	勾选Danamic Web Module Versions为3.0
	勾选Java为 1.8
	如下图所示：
	![](http://i4.buimg.com/4851/d37f161f8918df45.png)
(4) Properties -> Deployment Assembly 
	查看是否有加入Maven Dependencies以及对应的路径是否一样
	示例：
	![](http://i4.buimg.com/4851/22e55d515aa09e6f.png)

3 如果发现Properties中没有Deployment Assembly
解决方法：
(1) 在该项目的工作区文件夹找到.project文件,用文本编辑器打开
(2) 在文件内添加如下代码：
```
<nature>org.eclipse.wst.common.modulecore.ModuleCoreNature</nature>
```
(3) 重启eclipse可以在Properties中看到Deployment Assembly

以上配置好之后可以试着Run as -> Run On Server,看是否能在tomcat中跑起来。