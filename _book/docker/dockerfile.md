## Dockerfile 

    Dockerfile docker镜像的构建文件
     
    5.1. 编写Dockerfile
    
         5.1.1. 保留字节指令为大写,并且后面要跟随参数
         5.1.2. 指令从上往下依次执行
         5.1.3. #表示注视
         5.1.4. 会创建新的镜像层、并对镜像进行提交
         
    5.2. dockerfile 保留字解析 
    
         5.2.1. FROM 基础镜像
         5.2.2. MAINTAINER 维护者的姓名和邮箱地址
         5.2.3. RUN 容器构建时需要运行的命令
         5.2.4. EXPOSE 开放的端口信息
         5.2.5. WORKDIR 终端默认的登陆目录,落脚点-无指定，则是根目录 
         5.2.6. ENV 构建过程中设置环境变量   ENV MY_PATH /usr/mytest
         5.2.7. ADD 把对应的文件拷贝进入镜像 【自带解压缩】
         5.2.8. COPY 把对应的文件拷贝进入镜像
         5.2.9. VOLUMN 卷加载
         5.2.10. CMD 执行命令,多个CDM最后一个有效,会被docker run 之后的参数替换
         5.2.11. ENTRYPOINT  指令容器启动的时候要运行的命令 目的与CMD一样，但是会追加
         5.2.12. ONBUILD 触发器，只要子镜像build的时候，触发用的


​    
    5.3. docker build
    
         5.3.1. [mycentos](https://github.com/ylzyqt/summarize-integration/blob/master/docker/dockfile/mycentos)
         
         docker build -f Dockerfile -t namespace/centos:tag .
           
    5.4. 执行