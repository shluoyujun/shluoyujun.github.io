---
title: Java异常处理最佳实践
date: 2019-07-06 19:13:25
categories:
	 - developing
tags: [java,exception]
---
Java异常的分类如下图所示：
<!-- more --> 
<img src="/img/java异常分类.png">

checked异常需要在代码中显示处理，否则会编译出错。checked异常进一步分为
（１）引起注意型，如SQLException,ClassNotFoundException
（２）坦然处置型，如UnAuthorizedException
unchecked异常是运行时异常，继承RuntimeException，不需要程序进行显示的捕捉和处理。unchecked异常进一步分为
（１）可预测异常，如IndexOutOfBoundsException,NullPointerException，此类异常不应该产生或抛出，而应该提前做好边界检查
（２）需捕获异常，如RPC调用的远程服务超时异常
（３）可透出异常，框架或系统产生的且会自行处理的异常，程序无需关心

Java异常处理应该遵守如下准则：
１　在finally中释放资源或使用try-with-resource语句
２　抛出异常应尽可能具体明确
３　在Javadoc里添加＠throws声明，描述什么样的情况会导致异常
４　使用log将异常信息同异常一起抛出
５　优先捕获更明确的异常
６　不要捕获Throwable
Throwable是所有异常（Exception）和错误（Error）的父类，虽然它能在catch从句中使用，但永远都不要这样做!
如果你在catch从句中使用了Throwable，它将不仅捕获所有异常，它还将捕获所有错误，错误是由JVM抛出的，用来表明不打算让应用来处理的严重错误。
OutOfMemoryError和StackOverflowError便是典型的例子，它们都是由于一些超出应用处理范围的情况导致的。
```
public void doNotCatchThrowable() {
    try {
        // do something
    } catch (Throwable t) {
        // don't do this!
    }
}
```
7 不要忽略异常
catch到的异常应该做相应处理，至少也要讲日志打印出来。
８　不要打印异常日志的同时将其抛出
这样会导致一个异常打印多个异常信息
９　包裹某个异常的同时不要丢弃它原本的异常消息

处理Java异常最重要的是明确什么时候应该向上抛出，什么时候应该捕获异常。

References
１《码出高效Java开发手册》
２https://stackify.com/best-practices-exceptions-java/
３https://zhuanlan.zhihu.com/p/56115804