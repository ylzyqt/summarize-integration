## summarize

 1. [install for mac](http://docker-cn.com/get-docker)  
 
    1.1 下载后, 按照默认安装即可
    
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
    
         2.2.1 `docker images` 查看本地所有的镜像 [-a查看全部][-q查看镜像id][-digests查看说明]
         
         2.2.2 `docker search tomcat` 搜索tomcat的版本信息[-s 30 查看30星以上的]  
         
         2.2.3 `docker pull tomcat:8.0.53`  下载tomcat:8.0.53版本的镜像，默认latest
         
         2.2.4 `docker rmi image_id` 删除镜像[-f 强制删除]
         
    2.3 容器命令
         
         2.3.1 `docker run image_id` [-i 启动交互式][-t 启动伪终端][--name 重新命名别名][-d 后端运行]
                
                docker run -it -d --name test_name images_id
                
         2.3.2 `docker ps `  列出当前所有在运行的容器
         
         2.3.3  退出容器
                
                `exit` 直接退出容器,容器关闭
                  
                `command + p + q` 退出容器,容器依然在运行   
         
         2.3.4 启动容器
                
                `docker start container_id` 启动容器
                
                `docker restart container_id` 重启容器     
                
         2.3.5 停止容器
                
                `docker stop container_id` 停止容器
                
                `docker kill container_id` 强制停止容器  
                
         2.3.6 删除容器
              
                `docker rm container_id` 删除容器
                
         2.3.7 查看容器相关信息
         
                `docker logs -f container_id` 查看容器输出日志
                
                `docker stats [container_id]` 查看容器的性能问题 
                
                `docker inspect container_id` 查看容器相关的具体信息
                
                            
              
       
    
    