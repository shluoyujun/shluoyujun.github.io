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
+ Hive是一个数据仓库，存储大数据，主要用来做OLAP分析.
+ Hive定义了一种类似SQL的查询语言（HQL），将SQL转化为MapReduce任务在HDFS上执行，通常用于离线分析。
+ 数据的导入导出可以用工具sqoop，原理也是把命令翻译成MapReduce任务。

# HBase
+ HBase是什么
HBase是构建在HDFS上的分布式数据库，适用于OLAP任务。
+ 列式存储
HBase使用列式存储，相当于把mysql每一行的每一列拆开，然后通过rowkey关联起来。HBase中每一行是key-value的形式。
+ 列簇
可以定义列簇把相关列存储在一起。生产环境由于性能考虑和数据均衡考虑，一般只会用一个列簇，最多连个列簇。
+ rowkey的设计
HBase只能通过rowkey来查询，rowkey底层是B+数存储。
HBase提供三种查询方式：1）全表扫描，scan；2）根据一个rowkey查询；3）根据rowkey过滤的范围查询
+ LSM三层存储模型
数据先写到内存MemStore中，内存达到一定阈值再刷写到硬盘StoreFile中，再满足一定条件时，小的StoreFile会合并为大的StoreFile
+ 数据修改
可进行数据修改和删除
+ HBase架构
HMaster, HRegionServer, zookeeper
+ HRegionServer架构
HLog, WAL, MemStore, StoreFile
Region是HBase在rowkey上的切分，每个Region都可以通过startKey和endKey来确定rowkey范围，一个HRegionServer可能有多个Region。
rowkey需考虑散列性
+ 读取和写入流程


