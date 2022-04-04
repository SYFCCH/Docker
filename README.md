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



# Docker启动命令
systemctl start docker


# Docker为什么比虚拟机快
1.docker有比虚拟机更少的抽象层，不需要硬件资源初始化
2.docker利用的是宿主机的内核，而不需要重新加载操作系统OS内核

# Docker基本命令
启动docker: systemctl start docker
停止docker: systemctl stop docker
重启docker: systemctl restart docker
查看docker状态: systemctl status docker
开机启动: systemctl enable docker
查看docker概要信息: docker info
查看docker总体帮助文档: docker --help
查看docker命令帮助文档: docker 具体命令 --help



