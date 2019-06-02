---
title: docker常用命令
date: 2017-08-05 12:16:50
categories:
	 - command
tags: [linux, docker]
---

docker的安装以及一些配置参考
```
https://github.com/widuu/chinese_docker/blob/master/installation/ubuntu.md#Ubuntu%E5%AE%89%E8%A3%85Docker
```

<!--more-->

目录挂载
```
mkdir /work
sudo mkfs.ext4 /dev/vdc
sudo mount /dev/vdc /work
```
或者解除挂载
```
sudo umount  /dev/vdc /work
```
查看挂载情况
```
df -h
```

可参考
```
https://gist.github.com/gaoyifan/019ad7766f030ab5be50
```

更改镜像和容器的保存路径
```
sudo docker info | grep "Docker Root Dir" 查看存储位置
sudo vi /etc/default/docker
```
添加一行
```
DOCKER_OPTS="-g /mnt/docker"
sudo service docker restart
```

查看docker信息
```
docker info
```

查看运行中的容器
```
docker ps
```

查看所有容器
```
docker ps -a
```

查看本地镜像
```
docker images
```
删除镜像
```
docker rmi $imagename
```

停止一个正在运行的容器
```
docker stop $dockername
```

删除所有停止的容器
```
docker rm $(docker ps -a -q)
```

启动一个容器
```
docker start $dockername
```

进入一个容器
```
docker exec -i -t $dockername /bin/sh
```
docker run的参数说明，例如有用命令启动一个容器
```
docker run --name $"dDocker" -d -p 8080:8888 -v /home/tensorflow:/home/jovyan/work jupyter/tensorflow-notebook start-notebook.sh --NotebookApp.token=''
```

--name 为容器指定一个名字，如果未指定会随机分配
-d 保持后台运行
-p 8080:8888 端口映射，8080是宿主机器的端口号，8888是docker端口号，访问时输入 [宿主机器ip：8080]
-v /home/tensorflow:/work/jovnan 目录映射，可以理解为共享目录。docker容器是临时的，这个参数为了是代码和数据持久化保存。
jupyter/tensorflow-notebook 镜像名称，如果本地不存在，docker会自动从hub.docker.com上获取

常见问题：
1 Couldn’t connect to Docker daemon at http+unix://var/run/docker.sock - is it running? 
有次重启虚拟机后突然遇到这个问题，解决方法：

```
sudo vi /etc/default/docker
```

添加一行

```
DOCKER_OPTS="-H tcp://127.0.0.1:4243 -H unix:///var/run/docker.sock"
```

再重启docker服务

```
sudo service docker restart
```

note: 重启机器的之前最好先把运行中的docker容器停了
