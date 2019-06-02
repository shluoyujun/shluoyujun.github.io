---
title: ubuntu安装mysql并开启远程连接
date: 2017-06-16 22:53:19
categories:
	 - environment
tags: [linux, mysql]
---
```
sudo apt-get install mysql-server
sudo apt-get install mysql-client
sudo apt-get install libmysqlclient-dev
```
<!-- more --> 
安装过程中会提示设置密码什么的，注意设置了不要忘了，安装完成之后可以使用如下命令来检查是否安装成功：
```
sudo netstat -tap | grep mysql
```

通过上述命令检查之后，如果看到有mysql 的socket处于 listen 状态则表示安装成功。
登陆mysql数据库可以通过如下命令：
```
mysql -u root -p
```

开启远程服务

例如，你想root使用123456从任何主机连接到mysql服务器。

1 首先，赋给root用户权限
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

2 修改my.cnf文件

编辑文件
```
sudo vi /etc/mysql/my.cnf
```
注释掉这句，127.0.0.1是只允许本地访问
```
#bind-address = 127.0.0.1
```

3 重启mysql服务
```
sudo /etc/init.d/mysql restart
```