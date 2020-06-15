# sonarqube-docker

### 简介

使用`docker`一键配置`sonarqube`，数据库为`postgres`

版本：

`sonarqube: 7.9.2-community`

`postgres: 12.1`

### 默认配置
默认数据库配置
```
username: docker
password: docker
database: docker
```
你可以通过修改`docker-entrypoint-initdb.d/init-user-db.sh`中的数据库指令修改，然后修改`docker-compose.yml`中`sonarqube`配置下的`environment`来连接

### 使用方法
1. 安装docker
2. 安装docker-compose(一般默认安装了)
3. clone当前仓库到本地
4. `cd sonarqube-docker && mkdir dbdata`
5. 执行`chmod -R ugo+w sonar`
6. 在`docker-compose.yml`路径下执行 `docker-compose up -d`

此时访问`http://${ip}:9000`，便可打开sonarqube页面


### 问题
1. 如果新增文件或文件夹一定要确认访问权限 `ls -la`
2. `high disk watermark [90%] exceeded on`
    - 在配置中更新`sonar.properties`
    - [ES 内存错误时更改配置](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-cluster.html#disk-based-shard-allocation)
```
    docker exec -it ty-sonarqube_sonarqube_1 curl -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d'
    {
      "transient": {
        "cluster.routing.allocation.disk.watermark.low": "20gb",
        "cluster.routing.allocation.disk.watermark.high": "10gb",
        "cluster.routing.allocation.disk.watermark.flood_stage": "5gb",
        "cluster.info.update.interval": "1m"
      }
    }'
```


