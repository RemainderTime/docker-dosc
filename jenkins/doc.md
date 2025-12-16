更新时间:2025-12-16
## 说明
该docker-compose.yml贴合生产环境配置，
根据自己服务器配置调整yml中内存大小相关的配置以及文件夹路径
## 宿主机创建jenkins容器数据目录
```
mkdir -p /home/docker/jenkins/data/jenkins_home
chmod -R 777 /home/docker/jenkins/data/jenkins_home
```

## 宿主机创建maven仓库目录

```
mkdir -p /home/docker/jenkins/data/maven_repo
chmod -R 777 /home/docker/jenkins/data/maven_repo
```
