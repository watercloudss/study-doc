## CentOS 7.8安装docker

# 环境准备

1. 安装docker持久化包和yum工具包 `yum install -y yum-utils device-mapper-persistent-data lvm2`

- yum-utils 简化yum安装的工具包，后面会用到相关命令修改镜像加速，非必选
- device-mapper-persistent-data lvm2：安装docker数据存储的驱动包,必须安装

1. 修改镜像安装源到阿里云加速,默认是国外的下载比较慢 `yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo` yum自动选择最快的安装源 `yum makecache fast`

# 安装 docker

> docker 相关的命令会在后续文章中详细讲解

- 安装开源设区版本docker,视网速快慢，大根需要1-2分钟 `yum -y install docker-ce`
- 启动docker `service docker start`
- 查看docker版本，分两部分，客户端信息，服务端信息 `docker version`
- 下载hello-word镜像 `docker pull hello-word`