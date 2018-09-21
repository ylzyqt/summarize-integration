## summarize

 1. install 
 
 
      1.  安装版本 confluent ,参考官网 https://www.confluent.io/
      2.  sudo nohup wget http://packages.confluent.io/archive/4.0/confluent-oss-4.0.0-2.11.zip &
      
 2. config
 
 
      1. advertised.listener
      2. zookeeper
      3. log.dir
      
 3. start && stop 
      
      
      kafka start:  ./kafka-server-start -daemon ../etc/kafka/server.properties
      kafka stop :  ./kafka-server-stop 
      schema start: ./schema-registry-start -daemon ../etc/schema-registry/schema-registry.properties
      distributed start: ./connect-distributed -daemon ../etc/schema-registry/connect-avro-distributed.properties 
                
 4. crud in kafka
 
 
      1. create:
           ./kafka-topics --create --zookeeper zkAddress --replication-factor 2 --partitions 2 --topic mytopic
           
      2. delete
            sudo ./kafka-topics --delete --zookeeper 127.0.0.1:2181 --topic zhudongquan
           （1）登录zookeeper客户端：命令：./bin/zkCli.sh 
           （2）找到topic所在的目录：ls /brokers/topics
           （3）找到要删除的topic，执行命令：rmr /brokers/topics/【topic name】即可，此时topic被彻底删除。
            delete /brokers/topics/zhudongquan/partitions/0/state
            (4) 恢复误删 delete /admin/delete_topics/test
           
           
            正式环境删除命令:
            rmr /kafka/config/topics/data-backup.upay.order-transaction
            rmr /kafka/brokers/topics/data-backup.upay.order-transaction
            rmr /kafka/admin/delete_topics/data-backup.upay.order-transaction
           
      3. modify
           //修改过期时间
           ./kafka-topics --zookeeper zkAddress --alter --topic mytopic --config retention.ms=86400000
           
           //修改分区数
           ./kafka-topics  --zookeeper zkAddress --alter --topic mytopic --partitions 3
                             
           //修改可最大字节数
           ./kafka-configs --zookeeper zdAddress --entity-type topics --entity-name mytopic --alter --add-config max.message.bytes=3145728
           ./kafka-configs --zookeeper zkAddress --entity-type topics --entity-name mytopic --alter --add-config max.partition.fetch.bytes=3145728
           
           //[修改replicas数-此部分在新版本待校验](http://kafka.apache.org/documentation/#basic_ops_increase_replication_factor)
           increase-replication-factor.json
           {"version":1,"partitions":[{"topic":"springCloudBus","partition":0,"replicas":[0,2]}]}
           ./kafka-reassign-partitions --zookeeper zkAddress --reassignment-json-file increase-replication-factor.json --execute
           
      4. 查
           ./kafka-topics --list --zookeeper zkAddress
           ./kafka-topics --describe --zookeeper  zkAddress --topic mytopic    
           
      5. 消费
          ./kafka-console-consumer --bootstrap-server kafkaBroker --topic mytopic --from-beginning     
           
        
 5. kafka connector       
       
       
       (1) 查看kafka状态命令
           curl -H "Accept:application/json" localhost:8083/
       
       (2)查看kafka当前的connectos
           curl -H "Accept:application/json" localhost:8083/connectors/
       
       (3)开启kafka binlog connectors
       
       本地:
       curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d 
       '{ "name": "back", "config": { "connector.class": "io.debezium.connector.mysql.MySqlConnector", "tasks.max": "1", "database.hostname": "127.0.0.1", 
          "database.port": "3306", "database.user": "root", "database.password": "root", "database.server.id": "1", "database.server.name": "backstage",
            "database.whitelist": "db0", "database.history.kafka.bootstrap.servers": "localhost:9092", "database.history.kafka.topic": "schema-changes.back" } }’
           
       (4) 查看具体的connectors:
       curl -i -X GET -H "Accept:application/json" localhost:8083/connectors/test-connector
       
       (5) 详细列表
       由于Kafka Connect的目的是作为一个服务运行，提供了一个用于管理connector的REST API。默认情况下，此服务的端口是8083。以下是当前支持的终端入口：
       * GET /connectors - 返回活跃的connector列表
       * POST /connectors - 创建一个新的connector；请求的主体是一个包含字符串name字段和对象config字段（connector的配置参数）的JSON对象。
       * GET /connectors/{name} - 获取指定connector的信息
       * GET /connectors/{name}/config - 获取指定connector的配置参数
       * PUT /connectors/{name}/config - 更新指定connector的配置参数
       * GET /connectors/{name}/status - 获取connector的当前状态，包括它是否正在运行，失败，暂停等。
       * GET /connectors/{name}/tasks - 获取当前正在运行的connector的任务列表。
       * GET /connectors/{name}/tasks/{taskid}/status - 获取任务的当前状态，包括是否是运行中的，失败的，暂停的等，
       * PUT /connectors/{name}/pause - 暂停连接器和它的任务，停止消息处理，直到connector恢复。
       * PUT /connectors/{name}/resume - 恢复暂停的connector（如果connector没有暂停，则什么都不做）
       * POST /connectors/{name}/restart - 重启connector（connector已故障）
       * POST /connectors/{name}/tasks/{taskId}/restart - 重启单个任务 (通常这个任务已失败)
       * DELETE /connectors/{name} - 删除connector, 停止所有的
    
    
    