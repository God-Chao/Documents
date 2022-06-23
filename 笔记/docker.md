# Docker

## 1.安装Docker

```bash
# 1.yum包更新到最新
yum update -y
# 2.安装需要的软件包，yum-util提供yun-config-manager功能，另外两个是devicemapper驱动依赖的
yum install -y yum-utils device-mapper-persistent-data lvm2
# 3.设置yum源
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 4.安装docker
yum install -y docker-ce
# 5.查看docker版本
docker -v
```

## 2.镜像命令

```bash
# 查看本地镜像
docker images
# 搜索镜像
docker search 搜索内容
# 拉取镜像
docker pull 镜像名:版本号

# 查看本地镜像id
docker images -q

# 删除镜像
docker rmi 容器id
```

## 3.容器命令

```bash
# 查看容器
docker ps  #查看正在运行的容器
docker ps -a  #查看所有容器
# 创建并启动容器
docker run 参数
-i 保持容器运行，退出容器后自动关闭
-t 为容器重新分配一个伪输入终端
-d 后台运行容器，需要使用docker exec进入容器
-it 交互式容器
-id 守护式容器
--name 为创建的容器命名

# 进入容器
docker exec 参数

# 创建一个后台运行的容器
docker run -id --name 容器名称 镜像名称:版本号

# 容器的启动与删除
docker start 容器名称
docker stop 容器名称
docker restart 容器名称
docker rm 容器名称

# 查看容器信息
docker inspect 容器名称

# 设置容器自启动
docker update 容器名称 --restart=always
```



## 4.Docker安装mysql

```bash
# 1.拉取mysql最新镜像
docker pull mysql:latest
# 2.查看镜像是否下载成功
docker images
# 3.创建并运行mysql容器
docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql
-> docker run : 创建并运行一个容器
-> –-name : 给容器起一个名字, 比如叫做 mysql
-> -p : 将宿主机端口与容器端口映射, 冒号左侧是宿主机端口, 右侧是docker容器端口
-> mysql : 镜像名称
# 4.检查容器是否启动成功
docker ps -a

# 进入mysql命令行
# 1.查看mysql容器id
docker ps -a
# 2.进入mysql容器命令行
docker exec -it 容器id bash
# 3.登录mysql
mysql -u root -p
# 输入quit退出mysql命令行，返回容器命令行
# 输入exit退出容器命令行，回到linux命令行
```



## 5.Docker安装redis

```bash
# 1.拉取redis最新镜像
docker pull redis:latest
# 2.查看镜像是否下载成功
docker images
# 3.创建并运行redis容器
docker run -itd --name redis -p 6379:6379 redis
-> docker run : 创建并运行一个容器
-> –-name : 给容器起一个名字, 比如叫做 redis
-> -p : 将宿主机端口与容器端口映射, 冒号左侧是宿主机端口, 右侧是docker容器端口
-> redis : 镜像名称
# 4.检查容器是否启动成功
docker ps -a

# 进入redis命令行
# 1.查看redis容器id
docker ps -a
# 2.进入redis容器命令行
docker exec -it 容器id bash
# 3.打开redis客户端
redis-cli
# 输入quit退出redis命令行，返回容器命令行
# 输入exit退出容器命令行，回到linux命令行
```



## 6.Docker安装RabbitMQ

```bash
# 1.拉取rabbitmq最新镜像
docker pull rabbitmq:latest
# 2.查看镜像是否下载成功
docker images
# 3.创建并运行rabbitmq容器
docker run --name rabbitmq -p 15672:15672 -p 5672:5672 -d rabbitmq
-> docker run : 创建并运行一个容器
-> –-name : 给容器起一个名字, 比如叫做 rabbitmq
-> 第一个-p ：用于页面访问使用
-> 第二个-p ：用于生产和消费端使用（也就是再代码里使用）
-> rabbitmq : 镜像名称
-> d：后台运行
# 4.检查容器是否启动成功
docker ps -a
# 5.进入rabbitmq容器命令行
docker exec -it 容器id bash
# 6.下载图形插件
rabbitmq-plugins enable rabbitmq_management
# 7.访问：ip:15672
```



## 7.Docker部署jar包

```bash
# 1.将jar包传输到/Downloads/docker-files目录下（以test.jar为例）
# 2.在该目录下创建并编辑Dockerfile文件
vim Dockerfile
# 3.输入以下内容
FROM java:8  # 指定jdk版本，会自动在docker中pull对应的镜像
MAINTAINER Chao <chao-j@qq.com>  # 指定作者和邮箱
ADD test.jar test.jar  # 将该jar包添加到docker镜像中，左边为源文件名，右边为镜像名
ENTRYPOINT ["java","-jar","test.jar"]  # jar的运行命令
# 4.打包镜像
docker build -t test .
# 5.输入docker images查看镜像是否正常创建
# 6.创建并运行容器
docker run -it -d --name test -p 8081:8080 test  # 这里左边的端口为外部访问的端口，右边为容器内容端口（因为tomcat默认为8080，所以此处最好不改）
# 7.调用接口测试是否部署成功
# 8.查看日志
docker logs test
```



## 8.Docker安装nginx

```bash
# 1.拉取镜像
docker pull nginx:latest
# 2.创建好目录
nginx
- conf
	- nginx.conf
- html
	- index.html
- logs
# 3.将以下内容复制进nginx.conf（官方配置，可先运行一个nginx容器，在容器/etc/nginx/nginx.conf中可找到）
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
# 4.在nginx目录下运行容器（挂载对应的目录和文件）
docker run --name nginx -p 80:80 -d \
-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf \
-v $PWD/logs:/var/log/nginx \
-v $PWD/html:/usr/share/nginx/html \
nginx
# 5.访问ip地址查看是否启动成功
```

