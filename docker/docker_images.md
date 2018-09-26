## summarize 

    5.1 elasticsearch:  
         
         5.1.1 下载:   docker pull elasticsearch:5.4.2
         
         5.1.2 启动:   docker run -d -p 9200:9200 -p 9300:9300 --name elasticsearch  elasticsearch:5.4.2
         
       
    
    5.2 kafka 
    
         5.2.1 下载:   docker pull spotify/kafka
         
         5.2.2 启动:   docker run -d -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=127.0.0.1
                      --env ADVERTISED_PORT=9092 spotify/kafka  
   
         
   