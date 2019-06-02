---
title: mysql一种千万数量级表的join方法
date: 2017-07-18 20:25:52
categories:
	 - performance
tags: mysql
---
mysql中, join, left join, right join都可以将两张表连接起来，但如果表中的数据太多，例如两张表中都有1000w+的数据，直接join一定会出错。
<!-- more --> 
一种批量处理的方法是，每次从一张表中load若干行数据（limit m,n），和另一张做join, 结果保存到一张新表里。
可以写一个程序或脚本来处理，基本语句如下：
```
sql1 = "insert ignore into QA select t.id,t.title, t.body, Answers.body,t.tags from (select Questions.id,Questions.title,Questions.body,Questions.answerid,Questions.tags from Questions limit "
sql2 = ",10000) as t left join Answers on t.answerid=Answers.id"
i=0
while(i<maxlen):
	exesql=sql1+str(i)+sql2
	i=i+10000
	cur.execute(exesql)
	conn.commit()
```