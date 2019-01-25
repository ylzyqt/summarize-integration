## docker基本命令 



### 1. 帮助命令

```
1. `docker version`  查看版本
2. `docker info` 查看详情
3. `docker --help` 查看帮助
```

### 2. 镜像命令

```
1. `docker images` 查看本地所有的镜像 [-a查看全部][-q查看镜像id][-digests查看说明]
2. `docker search tomcat` 搜索tomcat的版本信息[-s 30 查看30星以上的]  
3. `docker pull tomcat:8.0.53`  下载tomcat:8.0.53版本的镜像，默认latest
4. `docker rmi image_id` 删除镜像[-f 强制删除]
5.  提交镜像
        docker commit -m 'message' container_id  namespace/name:version  
6.  提交到仓库
        docker push namespace/name  即可提交(前提:需要登陆)  
```



### 3. 容器命令

```
1. `docker run image_id` [-i 启动交互式][-t 启动伪终端][--name 重新命名别名][-d 以守护进程的方式启动][-p 端口映射]
            docker run -it -d --name test_name -p 8080:8080 images_id
            
2. `docker ps `  列出当前所有在运行的容器
     
3.  退出容器
            `exit` 直接退出容器,容器关闭
            `command + p + q` 退出容器,容器依然在运行   
     
4. 启动容器
            `docker start container_id` 启动容器
            `docker restart container_id` 重启容器     
            
5. 停止容器
            `docker stop container_id` 停止容器
            `docker kill container_id` 强制停止容器  
            
6. 删除容器
            `docker rm container_id` 删除容器
            
7. 查看容器相关信息
            `docker logs -f container_id` 查看容器输出日志
            `docker stats [container_id]` 查看容器的性能问题
            `docker top container_id` 查看容器里面的进行信息 
            `docker inspect container_id` 查看容器相关的具体信息
            
8. 进入容器
            `docker attach container_id` 重新进入容器里面
            `docker exec -it container_id /bin/bash` 在容器中执行某些任务,并不一定是进入这个终端       
            
9. 拷贝容器内的文件到诉宿主机器
            `docker cp 7dae8873c170:/app/bin/test.log /Users/****/Downloads/`    
            
10. 删除无用的镜像和容器       
            `sudo docker system prune -a`   
```