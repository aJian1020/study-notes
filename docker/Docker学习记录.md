##### Docker安装

###### windows7 安装

###### window10 安装

###### Centos7 安装

> 官方文档：https://docs.docker.com/engine/install/centos/#install-docker-engine

> 环境准备

```shell
# 系统内核
[root@aJian ~]# uname -r
3.10.0-1127.19.1.el7.x86_64
# 系统版本
[root@aJian ~]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

> 安装步骤

```shell
# 1.卸载旧版本
[root@aJian ~]# yum remove docker \
                   docker-client \
                   docker-client-latest \
                   docker-common \
                   docker-latest \
                   docker-latest-logrotate \
                   docker-logrotate \
                   docker-engine

# 2.安装所需要的安装包
[root@aJian ~]# yum install -y yum-utils

# 3.设置镜像源。使用阿里云镜像源。按照官方文档操作时，默认的是官方的镜像源，由于官方镜像源在国外，所以比较慢
[root@aJian ~]# yum-config-manager \
     --add-repo \
     http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# 4.安装最新版docker引擎。中途会出现需要输入y的步骤
[root@aJian ~]# yum install docker-ce docker-ce-cli containerd.io
 
# (可选项)安装指定版本docker引擎。VERSION_STRING：要安装的docker版本号。版本号通过第一个命令查询得出。
yum list docker-ce --showduplicates | sort -r
yum install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io

# 5.启动docker
[root@aJian ~]# systemctl start docker

# 6.测试docker是否启动成功
[root@aJian ~]# docker version
Client: Docker Engine - Community
 Version:           19.03.13    # docker的版本号
 API version:       1.40
 Go version:        go1.13.15   # go语言的版本号
 Git commit:        4484c46d9d
 Built:             Wed Sep 16 17:03:45 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community  # 社区版
 Engine:
  Version:          19.03.13
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       4484c46d9d
  Built:            Wed Sep 16 17:02:21 2020
  OS/Arch:          linux/amd64     # linux系统
  Experimental:     false
 containerd:
  Version:          1.3.7
  GitCommit:        8fba4e9a7d01810a393d5d25a3621dc101981175
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
  
 # 7.运行hello-world

```

![image-20201109162347006](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109162347006.png)

```shell
8. 查看hello-world镜像
[root@aJian ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        10 months ago       13.3kB
```

> 卸载docker

```shell
# 1.卸载docker引擎
[root@aJian ~]# yum remove docker-ce docker-ce-cli containerd.io
# 2.删除docker目录
[root@aJian ~]# rm -rf /var/lib/docker
```

***

###### Deepin20安装

***

##### 配置阿里云镜像加速

> 环境准备：需要具有阿里云的账号和密码

```shell
# 1.登录阿里云官网。地址：https://account.aliyun.com/login/qr_login.htm
```

![image-20201109164538967](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109164538967.png)

``` shell
# 2. 搜索容器镜像服务
```

![image-20201109164821937](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109164821937.png)

```shell
# 3. 根据阿里云文档进行操作
```

![image-20201109165404734](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109165404734.png)

```shell
# 4. 创建目录
[root@aJian ~]# mkdir -p /etc/docker

# 5. 创建daemon.json文件，并写入加速器地址
[root@aJian ~]# sudo tee /etc/docker/daemon.json <<-'EOF'
 {
   "registry-mirrors": ["https://6cxvmwxg.mirror.aliyuncs.com"]
 }
 EOF
{
  "registry-mirrors": ["https://6cxvmwxg.mirror.aliyuncs.com"]
}

# 6. 重启docker
[root@aJian ~]# systemctl daemon-reload
[root@aJian ~]# systemctl restart docker

# 7. 验证加速器地址是否配置成功
```

![image-20201109170014707](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109170014707.png)



>配置阿里云加速器地址的原因

```shell
# 前面配置了阿里云镜像源，采用阿里云镜像加速可以让镜像下载时变得更快。  
```

***

##### Docker命令

> 官网地址：https://docs.docker.com/engine/reference/run/

![image-20201109173331389](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201109173331389.png)

###### docker run

```shell
# 语法
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
options: 要进行的操作。
image: 要启动的镜像
tag:版本号
command:启动时要执行的命令

```



##### Docker仓库

##### Docker镜像

##### Docker容器

##### Dockerfile

##### 数据卷挂载

##### Docker网络原理

#####  IDEA整合Docker

##### Docker Compose

##### Docker Swarm

##### CI\CD Jenkins



