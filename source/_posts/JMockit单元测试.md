---
title: JMockit单元测试
date: 2019-07-03 17:12:06
categories:
	 - testing
tags: [java,testing,JMockit]
---

最近项目在进行代码质量的提升，而单元测试覆盖率是代码质量的标准之一，项目主要用到Jmockit进行测试用例的编写，借此机会全面学习一下。
<!-- more --> 
在代码中会有很多与其他组件或服务的交互，例如网络，数据库等，在测试环境下可能并不具备发起这些请求的条件，因此我们需要对这些依赖进行模拟（mock）,JMockit就是一个Java类、接口和对象的模拟工具，应用在程序的单元测试中。

JMockit有两种Mock方式
（1）Behaviour-oriented (Expecation & Verification)
类似黑盒，是基于代码执行的行为的Mock，由人工定义输入什么，返回什么，一般遵循Record-Reply-Verification流程
* 录制方法预期行为
* 真实调用
* 验证录制行为被调用

（2）State-oriented (MockUp<GenericType>)
类似白盒，可以直接改写被Mock方法的内部逻辑

1 @Injectable和@Tested
（1）@Injectable经常和@Tested一并使用
（2）@Tested表示被测试对象实例，只能作用于具体类，而不能作用于接口，因为一个接口可能有多个实现类，被测试的只能是实现改接口的某一具体类。
（3）如果该对象没有赋值，JMockit会去实例化它，若@Tested的构造函数有参数，则JMockit通过在测试属性&测试参数中查找@Injectable修饰的Mocked对象注入@Tested对象的构造函数来实例化，不然，则用无参构造函数来实例化。除了构造函数的注入，JMockit还会通过属性查找的方式，把@Injectable对象注入到@Tested对象中。

2 @Mocked和@Injectable的区别
两个注解都是告诉JMockit生成一个Mocked对象，但@Injectable只针对其修饰的实例，而@Mocked是针对其修饰类的所有实例
@Injectable对类的静态方法、构造函数没有影响

3 MockUp和@Mock
MockUp+@Mock是一种常见的Mock方式，可以对某个类中的某个方法进行改写。

4 Expectations
Expectations用于录制，主要有两种使用方式
（１）通过引用外部类的Mock对象（＠Mocked,@Injectable,@Capturing）来录制
（２）通过构建函数注入类/对象来录制

5 Mock方法的选择 
有些场景可以用多种方法进行Mock，可以针对需要选择最方便的一个。
（１）Mock类
可以用Expecations
```
new Expectations(Utils.class) {{

}};
```
也可以MockUp
```
new MockUp<Utils>() {
	@Mock
	public void method() {

    }
};
```
（２）Mock实例
用Expectations
```
Utils instance = new Utils();
// 直接把实例传给Expectations的构造函数即可Mock这个实例
new Expectations(instance) {
    {
    }
};
 ```
（３）Mock接口
用＠Injectable注入接口实例，再用Expecations Mock方法。
一般来说，接口是给类来依赖的，我们给测试类加上＠Tested，就可以让Jmockit做依赖注入。

References
http://jmockit.cn/index.htm
