---
title: ubuntu mysql修改数据存储位置
date: 2017-08-18 20:30:21
categories:
	 - environment
tags: [linux, mysql]
---

1 登陆mysql查看数据存储路径
```
mysql -uroot -p
show variables like '%datadir%';
```

<!-- more --> 

2 建立新的存储路径
```
mkdir -p /data/mysql
```

3 复制原有的数据到新的存储路径（不要用mv！）
```
cp -R /var/lib/mysql/. /data/mysql  #如果有隐藏文件要用.，不能用*
```

4 修改文件夹权限
```
sudo chown -R mysql:mysql /data/mysql
```

5 修改配置文件
```
sudo vi /etc/mysql/my.cnf
```

修改
```
datadir = /data/mysql
```


6 修改启动文件
```
sudo vi /etc/apparmor.d/usr.sbin.mysqld
```

修改
```
/var/lib/mysql r,
/var/lib/mysql/** rwk,
```

为
```
/data/mysql r,
/data/mysql/** rwk,
```

7 重启服务

```
sudo /etc/init.d/apparmor restart
sudo /etc/init.d/mysql restart
```