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




