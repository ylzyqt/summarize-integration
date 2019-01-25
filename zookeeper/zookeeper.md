## zookeeper



###  1: [下载地址](https://zookeeper.apache.org/releases.html)



### 2: 安装

步骤一: 解压缩

步骤二: 进入conf目录，拷贝zoo_sample.cfg -> zoo.cfg

步骤三: 修改zoo.cfg中的zookeeper数据存储位置: dataDir= zkdata

步骤四: 进入bin目录，执行 sh zkServer.sh start 启动    



### 3: 特殊配置

```
clientPortAddress=*.*.*.*   //当有多网卡的时候，指定启动网卡IP
```

