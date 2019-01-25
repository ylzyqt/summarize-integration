## Emqttd

#### 1. 技术选型


     1. http://www.emqtt.com/docs/v2/index.html 



#### 2. emqttd + protobuf

##### 2.1 install

```
https://github.com/google/protobuf/blob/master/README.md
找到  Protocol Complier Installation  下载 protobuf-cpp-***.tar.gz,下载后解压缩
```

##### 2.2 config

```
./configure

make

make check

make install

protoc -version  验证是否已经安装成功
```

##### 2.3 生成java文件

```
protoc --java_out=./ test.proto 即根据当前的proto文件，生成对应的java文件
```


