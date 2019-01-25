## kafka

#### 1. install


    安装版本 confluent ,参考官网 https://www.confluent.io/
    sudo nohup wget http://packages.confluent.io/archive/4.0/confluent-oss-4.0.0-2.11.zip &

#### 2.config


    1. advertised.listener
    2. zookeeper
    3. log.dir



#### 3.start && stop 

```
1: kafka start:  
 ./kafka-server-start -daemon ../etc/kafka/server.properties

2: kafka stop :  
 ./kafka-server-stop 

3: schema start: 
 ./schema-registry-start -daemon ../etc/schema-registry/schema-registry.properties

4: distributed start: 
./connect-distributed -daemon ../etc/schema-registry/connect-avro-distributed.properties 
```



#### 4. CRUD 



#### 4.1 create:

  ```
./kafka-topics --create \ 
               --zookeeper zkAddress \ 
               --replication-factor 2 \ 
               --partitions 2 --topic mytopic
  ```



#### 4.2 delete :

```
sudo ./kafka-topics --delete --zookeeper 127.0.0.1:2181 --topic mytopic

登录zookeeper客户端：命令：./bin/zkCli.sh

找到topic所在的目录：ls /brokers/topics

找到要删除的topic，执行命令：rmr /brokers/topics/【topic name】即可，此时topic被彻底删除。

delete /brokers/topics/mytopic/partitions/0/state

恢复误删 delete /admin/delete_topics/test
```



#### 4.3 Modify

```
//1 修改过期时间
./kafka-topics --zookeeper zkAddress --alter --topic mytopic --config   retention.ms=86400000

//2 修改分区数
./kafka-topics  --zookeeper zkAddress --alter --topic mytopic --partitions 3

//3 修改可最大字节数
./kafka-configs --zookeeper zdAddress --entity-type topics --entity-name mytopic --alter --add-config max.message.bytes=3145728

./kafka-configs --zookeeper zkAddress --entity-type topics --entity-name mytopic --alter --add-config max.partition.fetch.bytes=3145728

//4.[修改replicas数-此部分在新版本待校验]
(http://kafka.apache.org/documentation/#basic_ops_increase_replication_factor)

//5. increase-replication-factor.json
{"version":1,"partitions":[{"topic":"springCloudBus","partition":0,"replicas":[0,2]}]}
       ./kafka-reassign-partitions --zookeeper zkAddress --reassignment-json-file increase-replication-factor.json --execute
```



#### 4.4 search

    1. ./kafka-topics --list --zookeeper zkAddress
    
    2. ./kafka-topics --describe --zookeeper  zkAddress --topic mytopic    
           
    3. ./kafka-console-consumer --bootstrap-server kafkaBroker --topic mytopic --from-beginning     


​        