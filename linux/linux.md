## summarize

#### 常见命令列表

   1.  查看文件信息
        ls -lht
        du -d 1 -h | grep 'something to grep'
        du -h --max-depth=1
        df -h 
        
   2.  拷贝移动文件
        cp origin.jpg /Users/syst/idea.jpg
        mv origin.jpg /Users/idea.jpg
   
   3.  更改权限       
       chmod 777 a.txt
       chmod -R 777 aaa                修改文件夹权限
       chmod  600  test.pem     
       
   4.  查看进程
       ps -ef | grep java
       
   5.  查看端口
        netstat -ap | grep 6443
        
   6.  查找文件
        find / -name startup.sh              
    
   7.  滚动查看日志
        tail -f rpc-2016-12-29.0.log | grep --line-buffer "something to search" 
    
   8. mac别名
        vi ~/.bash_profile
        source .bash_profile
        使用alias -p查询是否生效 