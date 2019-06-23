---
title: Java反射初识
date: 2019-06-23 20:14:21
categories:
	 - developing
tags: [java,reflect]
---
学习反射能更深入的了解Java的编译，运行阶段，泛型等。周末看了一个讲解反射的课程，觉得讲的不错，适合入门。课程地址https://www.imooc.com/learn/199

＃Class的使用
Java中静态成员和基本数据类型不是对象，其他都是对象
类是java.lang.Class类的实例对象

实例对象的三种获取方式
Foo foo = new Foo();
Class c1 = Foo.class;
Class c2 = foo.getClass();
Class c3 = Class.forName("xx.xx.xx.Foo");
c1,c2,c3称为Foo类的类类型
可以通过类类型创建对象, 类需要有无参数的构造方法
Foo foo = (Foo)c1.newInsatance();

＃动态加载类
区分编译和运行
静态加载类　
Foo foo = new Foo();
动态加载类
Class.forName("类全称"）
编译时刻加载类是静态加载类，运行时刻加载类是动态加载类

如果一个类中涉及到多个类，此时将多个类向上提取接口（众类实现该接口），然后通过动态加载类的方式在运行的时候才创建对象不用的不需要编译就不会报错，这样底层不需要改动，每次增加一个类实现该接口标准就可以也不需要编译officebetter 只需编译新添加的类。

在设计方面，功能性的类，我们尽量去使用动态加载，而不使用静态加载，这样可以使程序更加灵活。

＃获取方法信息
Class类的基本API使用
获取类的信息，包括类类型，成员函数，成员变量
Class c = int.class;
c.getName();

＃获取成员变量构造函数信息
成员变量的反射
Filed[] fs = c.getDeclaredFields();
构造函数的反射
Constructor[] cs = c.geteclaredConstructors();

＃方法的反射
获取方法
方法的名称和方法的参数列表才能唯一决定某个方法
方法反射的操作
method.invoke(对象，参数列表)

＃通过反射了解集合泛型的本质
反射可以绕过编译
但Java中集合的泛型，是防止输入错误的，只在编译阶段有效，编译之后就无效了。