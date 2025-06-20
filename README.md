# docker-compose-linux

通过`docker-compose`编排一系列环境进行一键快速部署运行，小白运维神器。

### 一、环境准备

```shell
# 安装git命令： yum install -y git
git clone https://gitee.com/zhengqingya/docker-compose.git
cd docker-compose/Linux
```

### 二、运行服务

> 环境部署见每个服务下的`run.md`；
> eg: `Linux/portainer/run.md`

#### 数据库

1. [mysql](./Linux/mysql)
2. [mycat](./Linux/mycat)
3. [canal](./Linux/canal)
4. [oracle18c](./Linux/oracle18c)
5. [redis](./Linux/redis)
6. [couchbase](./Linux/couchbase)
7. [mongodb](./Linux/mongodb)
8. [seata](./Linux/seata)
9. [postgresql](./Linux/postgresql)
10. [yearning](./Linux/yearning)

#### 消息队列

1. [activemq](./Linux/activemq)
2. [kafka](./Linux/kafka)
3. [rabbitmq](./Linux/rabbitmq)
4. [rocketmq](./Linux/rocketmq)
5. [pulsar](./Linux/pulsar)

#### 日志系统

1. [elk](./Linux/elk)
2. [efk](./Linux/efk)
3. [elkf](./Linux/elkf)
4. [filebeat](./Linux/filebeat)
5. [graylog](./Linux/graylog)
6. [grafana_promtail_loki](./Linux/grafana_promtail_loki)
7. [grafana-promtail-loki-nginx-demo](./Linux/grafana-promtail-loki-nginx-demo)
8. [plumelog](./Linux/plumelog)
9. [zipkin](./Linux/zipkin)

#### CI/CD

1. [portainer](./Linux/portainer)
2. [jenkins](./Linux/jenkins)
3. [rancher](./Linux/rancher)
4. [gitlab](./Linux/gitlab)
5. [gogs](./Linux/gogs)
6. [sonarqube](./Linux/sonarqube)
7. [prometheus](./Linux/prometheus)
8. [grafana](./Linux/grafana)
9. [nginx](./Linux/nginx)

#### 文件存储

1. [fastdfs](./Linux/fastdfs)
2. [minio](./Linux/minio)
3. [baidupcs-web](./Linux/baidupcs-web)
4. [nextcloud](./Linux/nextcloud)

#### 其它

1. [elasticsearch](./Linux/elasticsearch)
2. [flowable](./Linux/flowable)
3. [jrebel](./Linux/jrebel)
4. [jumpserver](./Linux/jumpserver)
5. [nacos](./Linux/nacos)
6. [nps](./Linux/nps)
7. [opensumi-web](./Linux/opensumi-web)
8. [sentinel](./Linux/sentinel)
9. [tomcat](./Linux/tomcat)
10. [walle](./Linux/walle)
11. [xxl-job](./Linux/xxl-job)
12. [PowerJob](./Linux/PowerJob)
13. [yapi](./Linux/yapi)
14. [zookeeper](./Linux/zookeeper)
15. [jpom](./Linux/jpom)
16. [confluence](./Linux/confluence)
17. [jira](./Linux/jira)
18. [skywalking](./Linux/skywalking)

---

### windows 使用 docker-compose 安装开发环境系列

> 见[windows 使用 docker-compose 安装开发环境系列.md](./windows使用docker-compose安装开发环境系列.md)

---
#### Docker 命令
|命令|功能|示例|
 | ---- | ---- | ---- | ---- |
|docker| run	|启动一个新的容器并运行命令|	docker run -d ubuntu|
|docker| ps	|列出当前正在运行的容器|	docker ps|
|docker| ps -a	|列出所有容器（包括已停止的容器）|	docker ps -a|
|docker| build	|使用 Dockerfile 构建镜像|	docker build -t my-image|
|docker| images	|列出本地存储的所有镜像|	docker images|
|docker| pull	|从 Docker 仓库拉取镜像|	docker pull ubuntu|
|docker| push	|将镜像推送到 Docker 仓库	|docker push my-image|
|docker| exec	|在运行的容器中执行命令|	docker exec -it container_name bash|
|docker| stop	|停止一个或多个容器|	docker stop container_name|
|docker| start	|启动已停止的容器|	docker start container_name|
|docker| restart	|重启一个容器	|docker restart container_name|
|docker| rm	|删除一个或多个容器|	docker rm container_name|
|docker| rmi	|删除一个或多个镜像	|docker rmi my-image|
|docker| logs	|查看容器的日志|	docker logs container_name|
|docker| inspect	|获取容器或镜像的详细信息|	docker inspect container_name|
|docker| exec -it	|进入容器的交互式终端	|docker exec -it container_name /bin/bash|
|docker| network ls	|列出所有 Docker 网络	|docker network ls|
|docker| volume ls	|列出所有 Docker 卷|	docker volume ls|
|docker-compose |up	|启动多容器应用（从 docker-compose.yml 文件）	|docker-compose up|
|docker-compose |down	|停止并删除由 docker-compose 启动的容器、网络等	|docker-compose down|
|docker |info	|显示 Docker 系统的详细信息|	docker info|
|docker |version	|显示 Docker 客户端和守护进程的版本信息	|docker version|
|docker |stats	|显示容器的实时资源使用情况	|docker stats|
|docker |login	|登录 Docker 仓库|	docker login|
|docker |logout	|登出 Docker 仓库	|docker logout|

> 每天学习一点点，慢慢日积月累，你总会成为你喜欢的样子，加油。
