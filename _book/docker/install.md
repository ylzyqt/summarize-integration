## summarize


1. sudo apt-get remove docker docker-engine docker.io

2. sudo apt-get update

3. sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       software-properties-common
       
4. 如果3比较慢，执行4  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -       
 
5. sudo add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"

6. sudo apt-get update

7. apt-cache policy docker-ce

8. sudo apt-get install docker-ce=