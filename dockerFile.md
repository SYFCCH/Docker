# DockerFile
Dockerfile是用来构建Docker镜像的文本文件，是由一条条构建镜像所需的指令和参数构成的脚本。  
###### 三步骤  
编写Dockerfile文件->docker build命令构建镜像->docker run 镜像容器实例   
###### 基础知识  
1. 每条保留字指令都必须为大写字母且后面要跟随至少一个参数
2. 指令从上到下顺序执行
3. #表示注释 
4. 每条指令都会创建一个新的镜像层并对镜像进行提交  


# DockerFile常用保留字指令  
![img_97.png](img_97.png)  


#  案例  
让centos7内包含vim，jdk8，ifconfig    
1. 新建myfile文件夹,将jdk的Linux安装包传入    
``
mkdir /myfile
``
![img_98.png](img_98.png)  

2. vim Dockerfile   **D大写**  
```
FROM centos:7
MAINTAINER syf
ENV MYPATH /usr/local
WORKDIR $MYPATH
#安装vim编辑器
RUN yum -y install vim
#安装ifconfig命令查看网络IP
RUN yum -y install net-tools
#安装java8及lib库
RUN yum -y install glibc.i686
RUN mkdir /usr/local/java
#ADD 是相对路径jar,把jdk-8u171-linux-x64.tar.gz添加到容器中,安装包必须要和Dockerfile文件在同一位置
ADD jdk-8u171-linux-x64.tar.gz /usr/local/java/
#配置java环境变量
ENV JAVA_HOME /usr/local/java/jdk1.8.0_171
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib:$CLASSPATH
ENV PATH $JAVA_HOME/bin:$PATH
EXPOSE 80
CMD echo $MYPATH
CMD echo "success--------------ok"
CMD /bin/bash
```  

3. 构建docker build -t  新镜像名字:TAG . 
**TAG后面有个 空格加点 **

