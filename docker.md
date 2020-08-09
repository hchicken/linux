# DOCKER

## centos8安装docker

```bash
yum install docker -y
yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
dnf list docker-ce
dnf install docker-ce --nobest
ps -ef|grep docker
docker -v
systemctl enable --now docker
systemctl status docker
```

### docker 基本命令

* 查看镜像： docker images
* 删除指定id的镜像：docker rmi <image id>
* 删除所有镜像： docker rmi $(docker images -q)
* 强制删除镜像： docker rmi -f $(docker images -q)
* 停止所有容器： docker stop $(docker ps -a -q)
* 删除所有容器： docker rm $(docker ps -a -q)

### 安装redis

* -p:宿主机端口:容器端口
* --requirepass: 密码

```bash
docker run --name redis -p xxx:xxx -d --restart=always redis redis-server --requirepass "xxxx"
```

### 安装kafka

```bash
docker run  -d --name kafka \
-p 9092:9092 \
-e KAFKA_BROKER_ID=0 \
-e KAFKA_ZOOKEEPER_CONNECT=x.x.x.x:2181/kafka \
-e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://x.x.x.x:9092 \
-e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 \
-t wurstmeister/kafka
```

* 说明



### 安装zookeeper

```bash
docker run -itd --name zookeeper -p 2181:2181 wurstmeister/zookeeper
```

### 安装rabbit

```bash
docker pull rabbitmq
docker run -d -p 5672:5672 -p 15672:15672 --name rabbitmq rabbitmq
```