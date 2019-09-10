---
title: '初识sssd,ldap和kerberos'
date: 2019-08-01 21:52:57
categories:
	 - security
tags: [Hadoop, linux]
---
ldap+kerberos是hadoop这种多租户平台最常用的集中账号管理，认证和授权系统，本文对基本概念进行简单梳理。
<!-- more --> 

# ldap
存储租户账号

# kerberos
存储租户密码及组别关系
## kerberos架构
由server,client,application组成
### key distribution center(KDC)
密钥分发中心，负责管理发放票据，记录授权
### client
客户端。配置文件一般位于/etc/krb5.conf
### application
使用kerberos进行安全认证的应用
## 基本概念
### realm
kerberos管理领域的标识
### principal
当每添加一个用户或服务的时候都需要向kdc添加一条principal，principl的形式为 主名称／实例名@领域名
### password
客户的密码一般存在一个keytab文件中
### credential
credential是“证明某个人确定是他自己/某一种行为的确可以发生”的凭据。在不同的使用场景下， credential的具体含义也略有不同：
+ 对于某个principal个体而言，他的credential就是他的password
+ 在kerberos认证的环节中，credential就意味着各种各样的ticket

## 基本操作
客户端获取票据
kinit -kt /path/to/hadoop.keytab hadoop/主机名@HADOOP.COM
kinit对应的是向kdc获取TGT的步骤。它会向/etc/krb5.conf中指定的kdc server来发送请求。
再执行klist查看TGT请求结果

# System Security Services Dameon (SSSD)
一个守护进程，该进程可以用来访问多种验证服务器，如LDAP，Kerberos等，并提供授权。SSSD是介于本地用户和数据存储之间的进程，本地客户端首先连接SSSD，再由SSSD联系外部资源提供者(一台远程服务器)

* 避免了本地每个客户端程序对认证服务器大量连接，所有本地程序仅联系SSSD，由SSSD连接认证服务器或SSSD缓存，有效的降低了负载。
* 允许离线授权。SSSD可以缓存远程服务器的用户认证身份，这允许在远程认证服务器宕机是，继续成功授权用户访问必要的资源。


References
https://blog.csdn.net/liu16659/article/details/80997333 

