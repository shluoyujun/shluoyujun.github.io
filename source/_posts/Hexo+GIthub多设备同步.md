---
title: Hexo+Github多设备同步
date: 2019-06-02 16:32:29
categories:
	 - environment
tags: [hexo,github]
---

用Hexo+Github写博客最不方便的是，只能在一个设备（搭建Hexo）上进行博客更新。如果工作中用到多个设备，或者换了新电脑，项目迁移起来十分不便。
其实它最主要的问题在于Hexo的配置文件是保存在本地的，因此可以用Github解决这个问题。主要思路是，用master分支保存博客内容相关文件，用另一个分支保存Hexo相关配置。

<!-- more --> 

1 在配置Hexo的机器上完成hexo配置迁移
（1）Git clone github项目并创建新的分支hexo
```
https://github.com/shluoyujun/shluoyujun.github.io
```
（2）切换到hexo分支
（3）把Hexo配置文件夹里的文件全部拷贝到项目shluoyujun.github.io里
注意路径！！！例如hexo配置在/usr/hexo, github项目在/usr/shluoyujun.github.io
```
cp -R /usr/hexo/* /usr/shluoyujun.github.io

```
删除主题模板的.git文件。如果在新设备上hexo g发现这个错误warn no layout ..,应该是主题模板文件丢了，从网上再下一份或者在hexo机器上之前的配置再拷贝一遍即可。
（4）把修改提交到github上

2 在另外一台机器上配置
（1）搭建Hexo+Github的环境准备
安装nodejs,hexo,git
本地和github的连接. ssh key
（2）拉取github的代码，并切换到hexo分支
（3）在项目里npm install
现在就可以在新机器上写博客了，注意所有修改提交到hexo分支。

参考
https://www.cnblogs.com/LandWind/articles/8952362.html
https://blog.csdn.net/Monkey_LZL/article/details/60870891
https://www.jianshu.com/p/fceaf373d797