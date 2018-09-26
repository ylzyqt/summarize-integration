## summarize

 1. install 
    
    
     1.1  wget http://www.boutell.com/rinetd/http/rinetd.tar.gz
     
     1.2  tar zxvf rinetd.tar.gz
          make
          make install
          
     1.3  编辑配置
     
          vi /etc/rinetd.conf
          
     1.4  查询当前的连接信息
        
          sudo netstat -tanulp|grep rinetd
          
     1.5  启动rinetd
         
          sudo rinetd -c /etc/rinetd.conf                
 
        
       
    
    
    