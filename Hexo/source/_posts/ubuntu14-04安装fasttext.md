---
title: ubuntu14.04安装fasttext
date: 2017-06-16 22:40:06
categories:
	 - environment
tags: [linux,python,deeplearning]
---
```
sudo apt-get install python-numpy
sudo apt-get install python-scipy
```
<!-- more --> 
安装pip
```
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip -V #查看pip版本
```

安装Cpython
```
sudo pip install Cython --install-option="--no-cython-compile"
```

安装fasttext
```
sudo pip install fasttext
```