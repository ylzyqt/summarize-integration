## summarize

#### 常见命令列表

   1.  查看文件信息
   
   
        1.  ls -lht        
        2.  du -d 1 -h | grep 'something to grep'
        3.  du -h --max-depth=1
        4.  df -h 
        
   2.  拷贝移动文件
   
   
        1.  cp origin.jpg /Users/syst/idea.jpg
        2.  mv origin.jpg /Users/idea.jpg
   
   3.  更改权限
   
          
       1.  chmod 777 a.txt
       2.  chmod -R 777 aaa                修改文件夹权限
       3.  chmod  600  test.pem     
       
   4.  查看进程
   
   
       1.  ps -ef | grep java
       
   5.  查看端口
   
   
       1.  netstat -ap | grep 6443
        
   6.  查找文件
   
   
       1.  find / -name startup.sh              
    
   7.  滚动查看日志
   
   
       1.  tail -f rpc-2016-12-29.0.log | grep --line-buffer "something to search" 
    
   8. mac别名
   
   
        vi ~/.bash_profile
        
        source .bash_profile
        
        使用alias -p查询是否生效 