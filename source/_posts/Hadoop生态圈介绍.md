---
title: Hadoop生态圈介绍
date: 2019-06-29 18:20:04
categories:
	 - bigData
tags: [Hadoop]
---
作为Hadoop集群的运维工程师，学习Hadoop的目的是为了解业务。
<!-- more --> 
# Hive
Hive是一个数据仓库，存储大数据，主要用来做OLAP分析.
Hive定义了一种类似SQL的查询语言（HQL），将SQL转化为MapReduce任务在HDFS上执行，通常用于离线分析。
数据的导入导出可以用工具sqoop，原理也是把命令翻译成MapReduce任务。