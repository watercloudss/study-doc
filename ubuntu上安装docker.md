### ubuntu上安装docker

安装一些必要的系统工具

```bash
$ sudo apt-get update
$ sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common复制代码
```

安装 GPG 证书

```bash
$ curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -复制代码
```

写入软件源信息

```bash
$ sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"复制代码
```

更新软件源

```bash
$ sudo apt-get -y update复制代码
```

安装 Docker CE

```bash
$ sudo apt-get -y install docker-ce复制代码
```

### 加入 Docker 用户组

安装之后，默认情况下，Docker 命令会使用 Unix socket 与 Docker 引擎通讯，而只有 Root 用户和 Docker 组的用户才可以访问 Docker 引擎的 Unix socket，一般 Linux 系统上不会直接使用 Root 用户。因此，更好地做法是将需要使用 Docker 的用户加入 Docker 用户组。

- 建立 Docker 用户组

```bash
$ sudo groupadd docker复制代码
```

- 将用户加入 Docker 用户组

```bash
$ sudo usermod -aG docker '用户名'
```

#### Ubuntu 16.04+、CentOS 7 系统配置

- 编辑 daemon.json 配置文件

  ```
  $ sudo nano /etc/docker/daemon.json复制代码
  ```

- 添加以下代码

  ```
  {
    "registry-mirrors": [
      "镜像加速器地址"
    ]
  }复制代码
  ```

- 重启 Docker 服务

  ```
  $ sudo systemctl daemon-reload
  $ sudo systemctl restart docker
  ```

- 检查加速器是否生效

  ```
  $ docker info
  ```

  看到输出以下内容，说明镜像加速器配置成功

  ```
  Registry Mirrors:
   镜像加速器地址
  ```

# docker 安装 redis5.0.3

### 一、拉取官方5.0.3镜像

```
[root@localhost ~]# docker pull redis:5.0.3
```

#### 下载完成

```
[root@localhost ~]# docker pull redis:5.0.3
5.0.3: Pulling from library/redis
f7e2b70d04ae: Pull complete 
421427137c28: Pull complete 
4af7ef63ef0f: Pull complete 
b858087b3517: Pull complete 
2aaf1944f5eb: Pull complete 
8270b5c7b90d: Pull complete 
Digest: sha256:4be7fdb131e76a6c6231e820c60b8b12938cf1ff3d437da4871b9b2440f4e385
Status: Downloaded newer image for redis:5.0.3
```

### 二、创建挂载目录

#### 1、创建挂载文件夹

```
[root@localhost ~]# mkdir -p /usr/local/redis/data /usr/local/root/redis/conf
[root@localhost ~]# cd redis/
[root@localhost redis]# ls
conf  data
```

#### 2、创建redis.conf

#### 在/root/redis/conf目录中创建文件 redis.conf

```
touch redis.conf
```

#### 显示目录

```
[root@localhost redis]# cd conf/
[root@localhost conf]# ls
[root@localhost conf]# touch redis.conf
[root@localhost conf]# ls
redis.conf
[root@localhost conf]# 
```

### 三、创建redis 容器

```
docker run -d --name redis -p 6379:6379 -v /root/redis/conf/redis.conf:/redis.conf -v /root/redis/data:/data redis:5.0.3 redis-server --appendonly yes
```

#### 参数说明：

#### -d 后台运行

#### -p 端口映射到主机的端口

#### -v 将主机目录挂载到容器的目录

#### redis-server --appendonly yes : 在容器执行redis-server启动命令，并打开

#### redis持久化配置

docker pull mysql:8.0

docker run -p 3307:3306 --name mysql8.0 -e MYSQL_ROOT_PASSWORD=root -d mysql:8.0 备注： -p 将本地主机的端口映射到docker容器端口（因为本机的3306端口已被其它版本占用，所以使用3307） --name 容器名称命名 -e 配置信息，配置root密码 -d 镜像名称


yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo