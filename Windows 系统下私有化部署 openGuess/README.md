
Windows 系统下私有化部署 openGuess


## 安装
下载 openGuess 6.0.0 LTS 版本，下载链接：  https://opengauss.org/zh/download/  登录openGauss开源社区，选择对应平台的极简版安装包。 

详情查看 [获取安装包 | openGauss文档 | openGauss社区](https://docs.opengauss.org/zh/docs/6.0.0/docs/InstallationGuide/获取安装包.html) 



最简易的安装方式用docker拉取openGuess 镜像安装部署

安装docker之后要配置docker的镜像源，通常在这个目录下 /etc/docker/daemon.json 

```
{
    "registry-mirrors": [
        "https://docker.linkedbus.com",
        "https://docker.xuanyuan.me"
    ]
}

```

配置镜像源之后就可以用docker拉取openGuess 的镜像

```
docker pull enmotech/opengauss:latest 
或者指定版本
docker pull enmotech/opengauss:6.0.0
```

从容器外部连接容器数据库

```
docker run --name opengauss --privileged=true -d -e GS_PASSWORD=密码 -p 5432:5432 enmotech/opengauss:latest
```

## 测试
用docker ps 查看opengauss是否在运行

用docker logs 查看opengauss的运行日志，查看是否有报错

## 注意事项
openGauss的密码有复杂度要求，需要：密码长度8个字符以上，必须同时包含大小写英文字母，数字，以及特殊符号
默认用户名是gaussdb

注：在服务器部署要开放5432端口

注：高斯数据库没有后置处理，对于char类型字段会自动填充空格，比如char(6)类型，填写长度为4 的 就会多两个空格填充