---
title: python开发环境配置
date: 2018-06-23 22:03:36
categories:
	 - environment
tags: [ubuntu, python]
---

1 安装virtualenv
(1) 安装pip

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install python-pip
```

<!-- more -->
(2) 安装virtualenv

```
sudo apt-get install python-virtualenv
```

(3) 创建不同版本python环境
进入需要虚拟化环境的目录，如

```
cd /home/yujluo
```

运行命令

```
virtualenv -p /usr/bin/python3 py3env
```
-p指定python版本 py3env为虚拟的环境目录

激活环境

```
source /home/yujluo/py3env/activate
```

退出环境

```
deactivate
```

2 使用jupyter notebook

(1) 安装jupyter notebook
pip install jupyter notebook

(2) 开启notebook
进入工作目录，如

```
cd /home/yujluo
```

开启服务
jupyter notebook

(3) 远程访问jupyter notebook
最简单的是从本地建立一个ssh通道到服务器

```
ssh <用户名>@<ip地址> -L127.0.0.1:1234:127.0.0.1:8888
```
然后再本浏览器输入localhost:1234再在服务器上记下token输入就可以使用了。