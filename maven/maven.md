## summarize

#### config for mac

```
1. vi ~/.bash_profile
2. export M2_HOME=/Users/youUserLocation/Documents/apache-maven-3.5.4/
3. export PATH=$PATH:$M2_HOME/bin
```



#### 基本命令

````
1. 打包并忽略测试  
        maven clean install -DskipTests
2. 设置主pom版本以及各个子pom版本
        mvn versions:set -DnewVersion=1.0
````



#### 创建模版工程

```
1. 创建模版工程:  mvn archetype:create-from-project
2. 找到上上一步中输出的archetype目录，然后执行 mvn install -DskipTests 
   即可安装archatype项目至本地
3. intellij删除已经配置好的archetype:
   /Users/*/Library/Caches/IntelliJIdea14/Maven/Indices/UserArchetypes.xml    
```