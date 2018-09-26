## summarize

 1. [install for mac](https://docs.docker.com/docker-for-mac/release-notes/)  
 
    1.1 下载(http://docker-cn.com/get-docker)后, 按照默认安装即可
    
    1.2 启动成功后，在控制台输入 docker version 即可查看docker版本
    
    1.3 与虚拟机的区别: 
    
        虚拟机: 资源占用多，步骤冗余，启动慢
        
        docker: 没有对硬件进行虚拟，每个容器互相之间隔离 (仓库/镜像/容器)
        
    1.4 mac使用阿里云镜像的时候，需要使用http,而不用https
       
 2. docker 基本命令
    
    2.1 帮助命令:  
         
         2.1.1 `docker version`  查看版本
         
         2.1.2 `docker info` 查看详情
         
         2.1.3 `docker --help` 查看帮助
    
    2.2 镜像命令 
    
         2.2.1 `docker images` 查看所有的镜像 [-a查看全部][-q查看镜像id][-digests查看说明]
         
         2.2.2 `docker search tomcat` 搜索tomcat的版本信息  
       
    
    