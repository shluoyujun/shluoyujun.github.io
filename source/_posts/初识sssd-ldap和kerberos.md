---
title: '初识sssd,ldap和kerberos'
date: 2019-08-01 21:52:57
categories:
	 - security
tags: [Hadoop, linux]
---
ldap+kerberos是hadoop这种多租户平台最常用的集中账号管理，认证和授权系统，本文对基本概念进行简单梳理。
<!-- more --> 

ldap
存储租户账号

kerberos
存储租户密码及组别关系
	key distribution center(KDC)
	application server
	client

principal

完整的Principal表示方法:
e1vis/admin@server116.example.com
用户  描述   Realm

System Security Services Dameon (SSSD)
一个守护进程，该进程可以用来访问多种验证服务器，如LDAP，Kerberos等，并提供授权。SSSD是介于本地用户和数据存储之间的进程，本地客户端首先连接SSSD，再由SSSD联系外部资源提供者(一台远程服务器)

* 避免了本地每个客户端程序对认证服务器大量连接，所有本地程序仅联系SSSD，由SSSD连接认证服务器或SSSD缓存，有效的降低了负载。
* 允许离线授权。SSSD可以缓存远程服务器的用户认证身份，这允许在远程认证服务器宕机是，继续成功授权用户访问必要的资源。


References
https://blog.csdn.net/liu16659/article/details/80997333 

