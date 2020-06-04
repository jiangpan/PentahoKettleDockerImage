## 在构建服务器上拉取构建脚本

```bash
git clone http://xxxxxxxx
```



## 在构建服务器git仓库中执行

- 清理本地修改
```bash
git checkout .
```

- 拉取最新代码

```bash
git pull 
```

- 给授权脚本增加可执行权限（可能需要）

```bash
chmod u+x docker-entrypoint.sh
```



## 使用Dockerfile构建docker镜像

构建镜像

```bash
docker build -t jiangpan/pentaho_kettle:v7.1.0.0-12 .
```


## 查看本地镜像

```bash
docker images
```


## 运行命令

- 设置jvm内存参数环境变量


```bash
PENTAHO_DI_JAVA_OPTIONS="-Xms1024m -Xmx2048m -XX:MaxPermSize=256m"
```



- 使用默认参数运行

```bash
docker run -d --rm -p 8181:8181 -e CARTE_PORT=8181 --name myPdiContainer jiangpan/pentaho_kettle:v7.1.0.0-12
```



- 设置carte名称，用户名、密码

```bash
docker run -d --rm -p=8180:8181 -e CARTE_NAME=mycarte -e CARTE_USER=cluster -e CARTE_PASSWORD=cluster jiangpan/pentaho_kettle:v7.1.0.0-12
```




- 设置carte名称，用户名、密码，carte监听的地址，carte连接的资源库的名称、用户、密码，jvm参数

```bash
docker run -d --rm -p 8181:8181 -e CARTE_NAME=mycarte -e CARTE_USER=cluster -e CARTE_PASSWORD=cluster -e CARTE_HOSTNAME=127.0.0.1 -e REP_NAME=dev  -e REP_USERNAME=admin -e REP_PASSWORD=admin -e PENTAHO_DI_JAVA_OPTIONS="-Xms1024m -Xmx2048m -XX:MaxPermSize=256m" jiangpan/pentaho_kettle:v7.1.0.0-12
```




- 运行容器命令

```bash
docker run -d --rm -p 8181:8181 -e CARTE_NAME=mycarte -e CARTE_USER=cluster -e CARTE_PASSWORD=cluster -e REP_NAME=dev  -e REP_USERNAME=admin -e REP_PASSWORD=admin -e PENTAHO_DI_JAVA_OPTIONS="-Xms1024m -Xmx2048m -XX:MaxPermSize=256m" jiangpan/pentaho_kettle:v7.1.0.0-12
```




## 环境变量参数列表

- `CARTE_NAME`：设置carte的的名称

- `CARTE_HOSTNAME`：设置carte的监听地址，默认为0.0.0.0
- `CARTE_USER`：设置carte的用户名
- `CARTE_PASSWORD`：设置carte的密码
- `REP_NAME`：设置资源库名称，务必与KETTLE_HOME目录下的repositories.xml中的名字保持一致
- `REP_USERNAME`：设置资源库用户名
- `REP_PASSWORD`：设置资源库密码
- `PENTAHO_DI_JAVA_OPTIONS`：设置jvm内存参数环境变量



## 运维命令

### 进入容器bash

```bash
docker exec -it pentaho_kettle /bin/bash
```

### 查看容器运行日志

```bash
docker logs -f pentaho_kettle
```
