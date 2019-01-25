## summarize

### 1. install

```
 wget http://www.boutell.com/rinetd/http/rinetd.tar.gz
```



### 2. install 

```
 tar zxvf rinetd.tar.gz
 make
 make install
```



### 3. 编辑配置

```
 vi /etc/rinetd.conf
```



### 4. 查询当前的连接信息

```
 sudo netstat -tanulp|grep rinetd
```



### 5.启动rinetd    

```
 sudo rinetd -c /etc/rinetd.conf                
```

   

  


​    