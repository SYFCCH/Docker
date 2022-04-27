# compose
###简介
Docker-Compose是Docker官方的开源项目，    
负责实现对Docker容器集群的快速编排。   
### 用途  
Compose允许用户通过一个单独的docker-compose.yml模板文件（YAML 格式）来定义一组相关联的应用容器为一个项目（project）。   

### 安装Docker compose
```
curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose    
chmod +x /usr/local/bin/docker-compose  
docker-compose --version  
```
![img_132.png](img_132.png)    



### Compose核心概念   
####  一文件
docker-compose.yml  

#### 两要素
###### 1.服务service      
一个个应用容器实例，比如订单微服务、库存微服务、mysql容器、nginx容器或者redis容器    
###### 2.工程project
由一组关联的应用容器组成的一个完整业务单元，在 docker-compose.yml 文件中定义。   



