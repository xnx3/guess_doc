
Windows 系统下私有化部署 openGuess


## 安装
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

openGauss的密码有复杂度要求，需要：密码长度8个字符以上，必须同时包含大小写英文字母，数字，以及特殊符号
默认用户名是gaussdb
```

**`docker run`**：用于运行一个新的容器。

**`--name opengauss`**：为容器指定一个名称为 `opengauss`，方便后续管理。如果未指定名称，Docker 会为容器自动分配一个随机名称。

**`-privileged=true`**：启用特权模式，允许容器访问宿主机的所有设备。通常用于需要更高权限的场景，比如访问内核模块、挂载文件系统等。对于 `opengauss` 数据库，这可能是为了确保容器内部有足够的权限运行数据库服务。

**`-d`**：后台运行容器（detach mode），即容器启动后不会锁定当前终端。

**`-e GS_PASSWORD=密码`**：设置环境变量 `GS_PASSWORD`，为 openGauss 数据库的超级用户的密码。 需要将 `密码` 替换为实际的密码值，例如 `Abcd123456@`。 

## 测试

用docker ps 查看opengauss是否在运行, 确保容器状态为 `running` 

用docker logs  opengauss  查看opengauss的运行日志，查看是否有报错

## 注意事项
注：在服务器部署要开放5432端口

注：高斯数据库没有后置处理，对于char类型字段会自动填充空格，比如char(6)类型，填写长度为4 的 就会多两个空格填充，在不考虑性能的前提下可以使用varchar

注：创建库的时候要加载插件，会有几秒的延迟，插件加载完成后可以正常使用gauss

注：mysql与gauss结构上略有差异

