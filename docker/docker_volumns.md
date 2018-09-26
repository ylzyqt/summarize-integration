## summarize 

   4.1  -v 数据卷挂载
      
      docker run -it -d -v /host_locatiojn:/container_location container_id  
      
      宿主机与容器直接实现数据共享
      :ro 容器内只读，不可写  [只允许主机单项做修改]
      :rw 容器内可读写       [允许主机容器双向修改]
   
   4.2 Dockerfile
      基本的dockerfile如下
      
      From centos
      
      Volume ["/datavolumn1","/datavolumn2"]
      
      CMD echo "finished ------------"
      
      CMD /bin/bash
      
      docker build -f Dockerfile -t namespace/centos .  
      当前镜像在创建的时候，即会创建目录 /datavlume1,/datavolumn2的目录
       
         
   