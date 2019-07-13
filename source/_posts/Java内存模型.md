---
title: Java内存模型
date: 2019-07-09 21:38:35
categories:
	 - developing
tags: [java, jvm]
---
Java内存模型的相关内容如图所示：
<!-- more --> 
<img src="/img/Java内存模型.png">
1 内存模型特征
原子性
* 除了long,double类型以外，Java的基本数据类型的读写都是原子性的
* synchronized保证原子性

可见性
* 当一个线程修改这个变量，其他线程可以立即得知
* volatile, synchronized, final保证可见性

有序性
* 如果在本线程内观察，所有操作都是有序的；如果在一个线程中观察另一个线程，所有操作都是无序的。即“线程内表现为串行的语义”，“指令重排”，“工作内存与主内存同步延迟”
* volitile, synchronized保证线程之间操作的有序性
* 先行发生规则

2 volatile
关键字volatile是Java虚拟机提供的最轻量级的同步机制。当一个变量被volatile修饰后具有两种特性
* 可见性
* 禁止指令重排序优化。使用内存屏障（Memory Barrier或Memory Fence，重排序时不能把后面的指令重排序到内存屏障之前的位置）禁止重排

注意，Java中的运算如value++并非原子操作（被编译成字节码时不止一条指令，当然严谨来说，只有一条字节码指令也并不一定就是一个原子操作），因此，基于volatile的变量在并发下并不总是安全的。只有在以下两个场景volatile可保证并发安全
* 运算结果不依赖变量的当前值，或者能够确保只有单一的线程修改变量的值
* 变量不需要与其他状态变量共同参与不变约束
