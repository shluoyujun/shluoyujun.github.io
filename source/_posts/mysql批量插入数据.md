---
title: mysql批量插入数据
date: 2017-07-18 20:22:44
categories:
	 - performance
tags: mysql
---
在SQL中我们通常用如下语句进行数据的插入:
```
insert into tablename (fieldname_1,...,filedname_n) value(value_1,...,value_n);
```
<!-- more --> 
但如果我们需要插入的数据量很大，这样的语句必然会出现性能问题。例如，我们需要插入1000w条的数据，那么就需要1000w条insert语句，并且每执行一条语句都需要commit一次才能真正插入到数据库中，其效率可想而知。因此，为解决这一性能瓶颈问题，MYSQL的官方文档也提出了批量插入的解决方法。

我们可以用如下语句进行数据的批量插入：
```
insert into tablename (fieldname_1,...,filedname_n) values (value_1,...,value_n),(value_1,...,value_n),...,(value_1,...,value_n);
```
多条数据用value隔开，执行后一次性次commit。

该方法涉及到的问题：
1  如果用java,请务必使用StringBuilder或者StringBuffered进行字符串拼接，千万不要用String，否则效率会非常低。
2  如果担心sql语句有最大长度限制，可以查看
```
C:\ProgramData\MySQL\MySQL Server 5.7
```
文件夹中的my.ini文件（这是个隐藏文件夹），找到max_allowed_packet属性，如果需要进行修改即可。