## rz

## 1. install for Mac

​     1.1  [item2 下载](http://www.iterm2.cn/download)

​     1.2  安装 lrzsz : brew install lrzsz

​     1.3  将当前目录下的item2* 文件拷贝到 /usr/local/bin/ 

​     1.4 修改文件可执行权限:

```
 chmod +x iterm2-send-zmodem.sh 
 chmod +x iterm2-recv-zmodem.sh
```



​     1.5 item 添加 triggers

```
"Preferences"面板->Profiles选项卡->Advanced->Triggers

Regular expression         Action                 Parameters
\*\*B0100              Run Silent Coprocess      /usr/local/bin/iterm2-send-zmodem.sh

\*\*B00000000000000     Run Silent Coprocess      /usr/local/bin/iterm2-recv-zmodem.sh 
```



# 2. install for ubuntu


    1. sudo apt-get update
    1. sudo apt-get install lrzsz      


​    
    