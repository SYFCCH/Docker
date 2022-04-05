# Docker

1. 容器与虚拟机比较  
1)虚拟机在本地系统看来只是一个文件，是主操作系统虚拟出来的从操作系统，一种带环境安装的解决方案，  虚拟一套硬件再运行一个完整操作系统，在该系统上再运行
进程缺点有三：资源占用多，启动慢，冗余步骤多  
2)Linux容器不是模拟一个完整的操作系统，而是对进程进行隔离  
Docker容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，Docker优势为启动快、占用体积小
没有进行硬件虚拟

#### Docker三要素
镜像(image)，容器(container)，仓库(repository)
###### 1.镜像
相当于java的类，是一个只读的模板，可以用来创建Docker容器，相当于一个root文件系统
###### 2.容器
相当于类的实例对象，用镜像创建的运行实例，每个容器都是相互隔离、保证安全的平台，可看成简易版的Linux环境
###### 3.仓库
相当于maven，集中存放镜像模板的地方

# Docker工作原理
Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上，然后通过Socket连接从客户端访问
![img.png](img.png)





# Docker为什么比虚拟机快
1.docker有比虚拟机更少的抽象层，不需要硬件资源初始化
2.docker利用的是宿主机的内核，而不需要重新加载操作系统OS内核

# Docker命令

**Docker启动命令**
`````
systemctl start docker
`````
---
**Docker基本命令**
````
启动docker: systemctl start docker  
停止docker: systemctl stop docker  
重启docker: systemctl restart docker  
查看docker状态: systemctl status docker  
开机启动docker: systemctl enable docker  
查看docker概要信息: docker info  
查看docker总体帮助文档: docker --help  
查看docker命令帮助文档: docker 具体命令 --help  
````
---
**镜像命令**
查看主机上的镜像: ```docker images```  
![img_1.png](img_1.png)
![img_2.png](img_2.png)  
同一仓库源可以有多个TAG版本,如果  不指定的话默认是用最新的  
````
docker search 镜像名  ： 查看官网的镜像   后面加 --limit N，可以只列出N个  
docker pull 镜像名字(:TAG)不指定TAG的话那就是下载最新版,可以用来下载镜像  
docker system df 可以查看docker空间  
docker rmi -f 镜像名/镜像ID 强制删除镜像![img_3.png](img_3.png)
````
面试题：docker虚悬镜像是什么？  
仓库名、标签都是<none>的镜像，俗称虚悬镜像dangling image
---
**Docker容器命令**  
1.启动容器
````
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
````
[OPTIONS]:

```
--name="容器名字" :指定容器新名称
-d: 后台运行
-i: 以交互模式启动容器，通常与-t同时使用
-t: 为容器重新分配一个伪输入终端，通常与-i同时使用
-P: 随机端口映射
-p: 指定端口映射  
```
![img_4.png](img_4.png)

例子: 以交互模式启动一个容器
```
docker run -it centos:centos7 /bin/bash
```
![img_5.png](img_5.png)  
2.查看当前正在运行的容器
```
新开一个终端然后输入
docker ps 
```
![img_6.png](img_6.png)
docker ps [OPTIONS]说明(常用)  
```
-a :列出当前所有运行的＋历史上运行过的  
-l :显示最近创建的容器  
-n :显示最近n个创建的容器  
-q :静默模式，只显示容器编号  
```
![img_7.png](img_7.png)
3.进入容器后退出容器  
* ```exit```，容器停止 
* ctrl + p + q,退出容器后，容器不停止  

4.其他容器操作
```
启动已停止运行的容器 docker start 容器ID/容器名
重启容器 docker restart 容器ID/容器名
停止容器 docker stop 容器ID/容器名
强制停止容器 docker kill 容器ID/容器名
删除已停止的容器 docker rm  容器ID
```
5.重要  
1) 启动守护式容器(后台服务器)  docker run -d 容器名  
大多数情况下我们都希望docker的服务是在后台运行的，不过一旦用后台，他前台没有，docker会觉得他没事情干就自杀了，直接就退出了
 所以我们还是以前台进入命令行告诉docker这个容器我们还在使用   
* 下面以redis来演示前后台
![img_8.png](img_8.png)
当然我们平常redis都是后台启动的，所以下面演示后台守护启动  
![img_9.png](img_9.png)

2) 浏览容器的日志信息
```
docker logs 容器id
```
![img_10.png](img_10.png)
3) 查看容器细节
```
docker inspect 容器ID
```
包含大量的json串
![img_11.png](img_11.png)  
**每一个容器**都是一个简易微小的Linux  
4) 进入正在运行的容器
```
docker run -it centos:centos7 /bin/bash
然后ctrl + p + q退出容器但是不停止容器的运行
```
![img_12.png](img_12.png)
接着如果我们要进入这个容器输入:  
``docker exec -it 进程名 /bin/bash``  
![img_13.png](img_13.png)
exec是在容器中打开新的终端，并且可以启动新的进程，用exit退出，不会导致容器的停止

还有一个指令可以进入正在运行的容器
``docker attach ``
attach直接进入终端，不会启动新的进程，用exit退出，容器停止