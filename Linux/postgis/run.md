# PostgreSQL

关系型数据库

### 运行

```shell
docker-compose -f docker-compose.yml -p postgresql up -d

# 若运行之后，postgresql启动日志报相关权限问题，给新产生的文件赋予权限
chmod -R 777 ./postgresql/data
```

连接

![postgresql-navicat-connection.png](images/postgresql-navicat-connection.png)

```shell
# 进入容器
docker exec -it postgresql /bin/bash
# 登录
psql -U postgres -W
# 查看版本
select version();
```

连接PGSQL报错column “datlastsysoid“ does not exist Line1:SELECT DISTINCT datalastsysoid FROM pg_database
注：PGSQL 15 版本会出现该问题

今天通过某数据库软件连接PG数据库，在数据库软件中报错如下图所示
解决方法1：升级navicat
将navicat升级到16.2以上版本

解决方法2：降级pgsql
老版本仍然可用

终极解决方法3：修改dll
找到navicat安装目录
有一个libcc.dll文件
1.备份这个文件

2.进入网站https://hexed.it/ 打开本地的libcc.dll 文件

3.右侧点击搜索，关键词“SELECT DISTINCT datlastsysoid”

4.找到之后，把‘datlastsysoid’这几个字，改成“dattablespace”

5.然后把文件下载回来，放回原处
