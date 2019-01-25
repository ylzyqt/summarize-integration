## summarize

### 1 . 安装[Docker For Mac](http://docker-cn.com/get-docker)  


    1.1. 下载后, 按照默认安装即可
    1.2. 启动成功后，在控制台输入 docker version 即可查看docker版本
    1.3. 与虚拟机的区别: 
         虚拟机: 资源占用多，步骤冗余，启动慢
         docker: 没有对硬件进行虚拟，每个容器互相之间隔离 (仓库/镜像/容器)
    1.4. mac使用阿里云镜像的时候，需要使用http,而不用https



### 2. [docker 基本命令](docker_basic.md)



### 3. Docker联合文件系统

```
分层镜像:
举例tomcat镜像
   tomcat 
     jdk8
      centos  
        kernel 
```



### 4. [数据卷](docker_volumns.md)

### 5. [Dockerfile](dockerfile.md) 



 


​                         
​           
​    

 