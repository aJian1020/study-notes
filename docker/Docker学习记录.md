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

> 官方文档：https://docs.docker.com/engine/install/debian/环境准备

> 环境准备

```shell
# 1.查看系统内核
bj9971020@bj9971020-PC:~$ uname -r
5.4.50-amd64-desktop
# 2.查看系统版本
bj9971020@bj9971020-PC:~$ cat /etc/os-release
PRETTY_NAME="Deepin 20"
NAME="Deepin"
VERSION_ID="20"
VERSION="20"
ID=Deepin
HOME_URL="https://www.deepin.org/"
BUG_REPORT_URL="https://bbs.deepin.org/"
```

> 安装步骤

```shell
# 1.删除旧的docker引擎
bj9971020@bj9971020-PC:~$ sudo apt-get remove docker docker-engine docker.io containerd runc

# 2.更新beepin系统安装包状态(这里不会真正的更新安装包，只是看看有没有安装包需要更新)
bj9971020@bj9971020-PC:~$ sudo apt-get update

# 3.安装所需要的包
bj9971020@bj9971020-PC:~$ sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg-agent \
     software-properties-common
# 4.添加 Docker 的官方 GPG 密钥
bj9971020@bj9971020-PC:~$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

# 5.验证密钥
bj9971020@bj9971020-PC:~$ sudo apt-key fingerprint 0EBFCD88

# 6.设置阿里云镜像地址
bj9971020@bj9971020-PC:~$ sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/debian stretch stable"
# 可能会出以下错误：
Traceback (most recent call last):
  File "/usr/bin/add-apt-repository", line 95, in <module>
    sp = SoftwareProperties(options=options)
  File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 109, in __init__
    self.reload_sourceslist()
  File "/usr/lib/python3/dist-packages/softwareproperties/SoftwareProperties.py", line 599, in reload_sourceslist
    self.distro.get_sources(self.sourceslist)    
  File "/usr/lib/python3/dist-packages/aptsources/distro.py", line 93, in get_sources
    (self.id, self.codename))
aptsources.distro.NoDistroTemplateException: Error: could not find a distribution template for Deepin/n/a
# 解决方法：
# 先进入sources.list文件
bj9971020@bj9971020-PC:~$ sudo vim /etc/apt/sources.list
# 然后再文件最后一行加上此地址。加上此地址后，不需要重复执行第六步
deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/debian stretch stable

# 7.默认安装最新版docker引擎
bj9971020@bj9971020-PC:~$ sudo apt-get update
bj9971020@bj9971020-PC:~$ sudo apt-get install docker-ce docker-ce-cli containerd.io
# (可选项)手动安装制定版本docker
# 查看docker版本
bj9971020@bj9971020-PC:~$ apt-cache madison docker-ce
# 安装指定版本 将VERSION_STRING替换为指定的版本号
bj9971020@bj9971020-PC:~$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io

# 8.测试docker是否安装成功
bj9971020@bj9971020-PC:~$ sudo docker version
Client: Docker Engine - Community
 Version:           19.03.13
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46d9d
 Built:             Wed Sep 16 17:03:03 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.13
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       4484c46d9d
  Built:            Wed Sep 16 17:01:33 2020
  OS/Arch:          linux/amd64
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

# 9.运行hello-world
bj9971020@bj9971020-PC:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:8c5aeeb6a5f3ba4883347d3747a7249f491766ca1caa47e5da5dfcf6b9b717c0
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

# 10.查看docker镜像
bj9971020@bj9971020-PC:~$ sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        10 months ago       13.3kB
```



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



