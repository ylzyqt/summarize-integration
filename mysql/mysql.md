## summarize

 1. 查询mysql慢查询时间设置 
    
    
    show variables like 'long%';
   
 2. 查询mysql是否打开慢查询日志   
 
     
     show variables like 'slow%';
    
 3: 查看连接数/状态   
 
    show processlist;
    
    show full processlist
    
 4: 查看最大连接数   
       
    show variables like '%max_connections%'
    
 5: 查询是否开启查询缓存
 
    show global variables like '%query_cache%'
    
 6: 是否开启Profile功能  
 
    SHOW VARIABLES LIKE '%pro%';
    
 7: 查看表的可释放空间
      
    select table_name,engine,table_rows,data_length+index_length length,DATA_FREE from
    information_schema.tables where  data_free !=0;
    
 8: binlog是否开启    
 
    show variables like 'log_bin';
    
 9: 开启binlog   
    
    /usr/local/mysql/my.cnf
    log-bin=mysql-bin  即可开启binlog;
 
 10. 设置service id
    
    /usr/local/mysql/my.cnf
    server_id=1  [取值1-232]  
    
 11. 设置binlog监听方式
    
    
    binlog_format = ROW
        
        
       
    
    
    