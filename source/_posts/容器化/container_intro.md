---
title: docker和k8s简介
date: 2019-12-15 13:49:07
tags:
  - docker
  - k8s
  - 容器化
categories: 容器化
cover: true
---

## Docker

### 什么是 docker

- docker 是一个开源的软件部署解决方案；
- docker 也是轻量级的应用容器框架；
- docker 可以打包、发布、运行任何的应用(Build,Ship,Run anywhere)。
- Docker 的基础是 Linux 容器(LXC)等技术。在 LXC 的基础上 Docker 进行了进一步的封装，让用户不需要去关心容器的管理，使得操作更为简便。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

### Docker vs 传统虚拟化

{% asset_img  virtualization.png 虚拟化  %}
{% asset_img  docker-1.png Docker  %}

> 容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，而传统方式则是在硬件层面实现。相比传统虚拟化技术,Docker 省去了操作系统的资源占用,达到了更高的资源利用率.

### 为什么用 Docker

#### - 高效、轻量

对比虚拟机，Docker 提供了一个经济、高效、可行的方案，可以节约出更多的资源投入到业务中去，让应用程序产生更高的效益。

#### - 快速、一致交付

在本地容器中得到一套标准的应用或服务的运行环境，简化开发的生命周期。对于整个应用迭代来说，更加适合持续集成( Continuous Integration )和持续交付( Continuous Delivery )。

#### - 跨平台部署和动态伸缩

很轻松的运行在开发者本地的电脑，云服务器，甚至是混合环境中；同时，轻量性和高可移植性能够很好的帮助我们完成应用的动态伸缩，大幅提高应用的健壮性。

#### - 完美契合微服务

微服务架构本身就意味着需要对若干个容器服务进行治理，每个微服务都应可以独立部署、扩容、监控,而 Docker 正是为此而生。

### QuickStart

1. 上手

假设我们需要在本地安装一个 mysql 数据库,如果是以前,我们需要下载、安装、配置等,但是有了 docker,简单执行一条命令即可:

```shell
$ docker run -p "3306:3306" --name my-mysql -e "MYSQL_ROOT_PASSWORD=123456" mysql
```

> `docker run`命令会为我们启动一个容器,其中`--name`参数指定了容器的名字,
> `-e`参数指定容器了的环境变量,Docker 会将环境变量设置到启动容器的环境变>量中.`-p`指定了容器的端口映射,Docker 容器运行在一个独立的网络环境中,需要通过端口映射来暴露服务.

可以看到输出结果如下:

```shell
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
743f2d6c1f65: Already exists
3f0c413ee255: Pull complete
aef1ef8f1aac: Pull complete
f9ee573e34cb: Pull complete
3f237e01f153: Pull complete
f9da32e8682a: Pull complete
4b8da52fb357: Pull complete
3416ca8f6890: Pull complete
786698c2d5de: Pull complete
4ddf84d07bd1: Pull complete
cd3aa23461b6: Pull complete
9f287a2a95ad: Pull complete
Digest: sha256:711df5b93720801b3a727864aba18c2ae46c07f9fe33d5ce9c1f5cbc2c035101
Status: Downloaded newer image for mysql:latest
Initializing database
2019-05-30T14:02:16.286390Z 0 [Warning] [MY-011070] [Server] 'Disabling symbolic links using --skip-symbolic-links (or equivalent) is the default. Consider not using this option as it' is deprecated and will be removed in a future release.
2019-05-30T14:02:16.286447Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.0.16) initializing of server in progress as process 28
2019-05-30T14:02:52.389697Z 5 [Warning] [MY-010453] [Server] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
2019-05-30T14:03:11.770831Z 0 [System] [MY-013170] [Server] /usr/sbin/mysqld (mysqld 8.0.16) initializing of server has completed
Database initialized
MySQL init process in progress...
MySQL init process in progress...
MySQL init process in progress...
2019-05-30T14:03:14.880462Z 0 [Warning] [MY-011070] [Server] 'Disabling symbolic links using --skip-symbolic-links (or equivalent) is the default. Consider not using this option as it' is deprecated and will be removed in a future release.
2019-05-30T14:03:14.880530Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.16) starting as process 79
2019-05-30T14:03:17.819022Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
2019-05-30T14:03:17.879218Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
2019-05-30T14:03:17.892082Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.16'  socket: '/var/run/mysqld/mysqld.sock'  port: 0  MySQL Community Server - GPL.
2019-05-30T14:03:17.950744Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: '/var/run/mysqld/mysqlx.sock'
Warning: Unable to load '/usr/share/zoneinfo/iso3166.tab' as time zone. Skipping it.
Warning: Unable to load '/usr/share/zoneinfo/leap-seconds.list' as time zone. Skipping it.
Warning: Unable to load '/usr/share/zoneinfo/zone.tab' as time zone. Skipping it.
Warning: Unable to load '/usr/share/zoneinfo/zone1970.tab' as time zone. Skipping it.

2019-05-30T14:03:31.156745Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.16)  MySQL Community Server - GPL.

MySQL init process done. Ready for start up.

2019-05-30T14:03:31.507777Z 0 [Warning] [MY-011070] [Server] 'Disabling symbolic links using --skip-symbolic-links (or equivalent) is the default. Consider not using this option as it' is deprecated and will be removed in a future release.
2019-05-30T14:03:31.507843Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.16) starting as process 1
2019-05-30T14:03:33.641301Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
2019-05-30T14:03:33.689783Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
2019-05-30T14:03:33.702444Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.16'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
2019-05-30T14:03:34.005880Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: '/var/run/mysqld/mysqlx.sock' bind-address: '::' port: 33060
```

在执行`docker run`时,Docker 首先会去 Docker Server 上查找对应的镜像,如果找不到,再去配置的镜像仓库服务器(Registry)查找,找了之后,再去对应的镜像仓库(Repository)下载镜像。可以看到镜像的下载是分了很多层的,这是因为 Docker 镜像都是由一层一层的只读层(Layer)堆叠而成的,而容器则是由多个只读层加上一层读写层。

启动成功后,我们尝试连接数据库:

```shell
$ mysql -h127.0.0.1 -P3306  -uroot -p123456
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 16
Server version: 8.0.16 MySQL Community Server - GPL

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

可以看到连接成功,mysql 版本号为最新 8.0.16,如果我们想切换到 5.6 版本呢?

```shell
docker run -p "3306:3306" --name my-mysql -e "MYSQL_ROOT_PASSWORD=123456" mysql:5.6
```

> mysql:5.6 中的 5.6 即是版本号,这里对应的其实是 Docker 镜像的标签(TAG),Docker 通过标签来对镜像的版本进行定义,如果不指定标签,则默认使用`latest`。

通过更换镜像的标签,我们可以运行不同版本的镜像而无需重复下载->配置->启动这一步骤,这便是 Docker 优于传统部署的地方。

2.  构建自己的镜像

接下来我们来写一个简单的计数器应用 k8s-demo 并将其构建为 Docker 镜像,应用使用 Go 语言开发,使用 go module 作为依赖管理工具,redis 作为存储,通过 REST API 对外暴露接口.

接口列表：

| 方法   | 路径   | 说明         |
| ------ | ------ | ------------ |
| GET    | /score | 获取当前分数 |
| PUT    | /score | 增加分数     |
| DELETE | /score | 减少分数     |

连接 Redis 的代码:

```shell
/*创建连接池*/
func createRedisPool() *redis.Pool {

    // 建立连接池
    rc := &redis.Pool{
        MaxIdle:     5,
        MaxActive:   10,
        IdleTimeout: 30 * time.Second,
        Wait:        true,
        Dial: func() (redis.Conn, error) {
            con, err := redis.Dial("tcp", os.Getenv("REDIS_HOST")+":"+os.Getenv("REDIS_PORT"),
                redis.DialPassword(os.Getenv("REDIS_PASSWORD")),
                redis.DialDatabase(0),
                redis.DialConnectTimeout(30*time.Second),
                redis.DialReadTimeout(30*time.Second),
                redis.DialWriteTimeout(30*time.Second))
            if err != nil {
                return nil, err
            }
            return con, nil
        },
    }

    return rc
}
```

其中连接 redis 的参数信息全部来自于系统的环境变量,这些都需要我们在启动的时候指定。

因为镜像中无法翻墙,所以我预先使用`go mod vendor`将依赖包下载到项目目录,在构建过程中直接使用项目目录的依赖。

Dockerfile:

```shell
# 起始镜像
FROM golang:1.12.1 AS build

# 工作目录
WORKDIR /home/app/k8s-demo

# 将当前目录下的所有文件添加至镜像中
ADD . .

# 执行打包命令 -mod=vendor 使用vendor打包 -installsuffix 加入C语言依赖库
# -a 如果文件已存在,强制重新构建
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -mod=vendor .

# golang打出来的包是不需要依赖golang环境的,所以我们可以使用多阶段构建来构建一个很轻量的包

FROM scratch AS prod

# 从build构建中复制文件到新的镜像中
COPY --from=build /home/app/k8s-demo/k8s-demo /home/app/k8s-demo

# 镜像入口
ENTRYPOINT ["/home/app/k8s-demo"]

# 暴露端口
EXPOSE 8081
```

> 一个标准的 Dockerfile 一般包含两部分
>
> 1. `FROM <IMAGE-NAME>` 表示镜像的基础镜像,我们已经知道一个 Docker 镜像是由多个只读层组成的,而构建一个新的镜像就相当于在原有的只读层基础上增加了若干层,其中,Dockerfile 中的每一行命令都对应一层.
> 2. `ENTRYPOINT ["COMMAND"]`或`CMD ["COMMAND"]` 是容器启动时运行的命令,每一个 Docker 容器都会有一个前台程序(即`ENTRYPOINT`或`CMD`指定的命令)在运行,可以认为这个前台程序的生命周期=容器的生命周期,程序停止,容器也就停止了。

使用`docker build`命令来构建镜像

```shell
$ docker build -t sivdead/k8s-demo:0.0.1 .
Sending build context to Docker daemon  10.83MB
Step 1/8 : FROM golang:1.12.1 AS build
 ---> 213fe73a3852
Step 2/8 : WORKDIR /home/app/k8s-demo
 ---> Using cache
 ---> d956750f77a6
Step 3/8 : ADD . .
 ---> 4af8a226fc44
Step 4/8 : RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -mod=vendor .
 ---> Running in 16d539aff688
Removing intermediate container 16d539aff688
 ---> 5b94044c0976
Step 5/8 : FROM scratch AS prod
 --->
Step 6/8 : COPY --from=build /home/app/k8s-demo/k8s-demo /usr/bin/k8s-demo
 ---> ff1e464c53d6
Step 7/8 : ENTRYPOINT ["/usr/bin/k8s-demo"]
 ---> Running in 154ccc263229
Removing intermediate container 154ccc263229
 ---> 7b79e52d4dca
Step 8/8 : EXPOSE 8081
 ---> Running in 7f089d0fe674
Removing intermediate container 7f089d0fe674
 ---> aff6c183e5a0
Successfully built aff6c183e5a0
Successfully tagged sivdead/k8s-demo:0.0.1

```

> 可以看到`FROM scratch`这里并没有生成 layer,这是因为 scratch 这个基础镜像比较特殊,它相当于什么都不做。

推送镜像到 Docker Hub(需要先注册 Docker Hub 账号)(可选)

```shell
$ docker push sivdead/k8s-demo:0.0.1
The push refers to repository [docker.io/sivdead/k8s-demo]
f2227fbd4aaf: Pushed
0.0.1: digest: sha256:2ccfa2b3cd0a10f867eb1bb7f637494ac2e38a0193736caf0c5c3ba2503e4277 size: 528
```

启动容器

因为应用依赖 redis,所以我们使用 docker-compose 来启动两个关联的容器(应用和 redis)。

docker-compose.yml

```shell
version: "3"
services:
  k8s-demo:
    image: sivdead/k8s-demo:0.0.3
    ports:
      - 8081:8081
    # 环境变量,这里配置的环境变量会在容器启动时配置到容器的环境变量中
    # 并由应用来引用
    environment:
      REDIS_HOST: k8s-demo-redis
      REDIS_PORT: 6379
      REDIS_PASSWORD: 123456
    networks:
      - k8s-demo
    depends_on:
      - k8s-demo-redis
  k8s-demo-redis:
    image: redis:4.0
    networks:
      - k8s-demo
    command: redis-server --requirepass 123456
#两个容器共享同一个网络来互相通信
networks:
  k8s-demo:
```

启动应用:

```shell
$ docker-compose up -d
Creating k8s-demo_k8s-demo-redis_1 ... done
Creating k8s-demo_k8s-demo_1       ... done
```

可以使用`docker-compose logs -f`来查看启动过程.

```shell
$ docker-compose logs -f
Attaching to k8s-demo_k8s-demo_1, k8s-demo_k8s-demo-redis_1
k8s-demo_1        | [GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.
k8s-demo_1        |
k8s-demo_1        | [GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
k8s-demo_1        |  - using env:       export GIN_MODE=release
k8s-demo_1        |  - using code:      gin.SetMode(gin.ReleaseMode)
k8s-demo_1        |
k8s-demo_1        | [GIN-debug] GET    /hello                    --> main.indexHandler.func1 (3 handlers)
k8s-demo_1        | [GIN-debug] PUT    /score/                   --> main.main.func1 (3 handlers)
k8s-demo_1        | [GIN-debug] GET    /score/                   --> main.main.func2 (3 handlers)
k8s-demo_1        | [GIN-debug] DELETE /score/                   --> main.main.func3 (3 handlers)
k8s-demo_1        | time="2019-05-27T17:17:24Z" level=info msg="listening at :8081"
k8s-demo_1        | [GIN-debug] Listening and serving HTTP on :8081
k8s-demo-redis_1  | 1:C 27 May 17:17:23.244 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
k8s-demo-redis_1  | 1:C 27 May 17:17:23.260 # Redis version=4.0.14, bits=64, commit=00000000, modified=0, pid=1, just started
k8s-demo-redis_1  | 1:C 27 May 17:17:23.260 # Configuration loaded
k8s-demo-redis_1  | 1:M 27 May 17:17:23.261 * Running mode=standalone, port=6379.
k8s-demo-redis_1  | 1:M 27 May 17:17:23.261 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
k8s-demo-redis_1  | 1:M 27 May 17:17:23.261 # Server initialized
k8s-demo-redis_1  | 1:M 27 May 17:17:23.261 # WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis. To fix this issue run the command 'echo never >
 /sys/kernel/mm/transparent_hugepage/enabled' as root, and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.
k8s-demo-redis_1  | 1:M 27 May 17:17:23.261 * Ready to accept connections

```

### Docker 架构

{% asset_img  docker结构.png Docker结构  %}

> Docker 使用 c/s 架构,client 实现容器和镜像的管理，为用户提供统一的操作界面.client 通过 REST API 与 server 进行通信,在构建容器时,server 首先从本地查找镜像,如果找不到,再从可用的 Docker regisry 上下载.client 和 server 可以运行在同一个机器,也可以跨主机远程通信.

### Docker 核心概念

#### - 镜像(image)

Docker 镜像就是一个只读的模板。例如：一个镜像可以包含一个完整的操作系统环境，里面仅安装了 Apache 或用户需要的其它应用程序。镜像可以用来创建 Docker 容器，一个镜像可以创建很多容器。Docker 提供了一个很简单的机制来创建镜像或者更新现有的镜像，用户甚至可以直接从其他人那里下载一个已经做好的镜像来直接使用。Docker 使用 UFS(Union File System)来将多个只读文件(Read only layer)堆叠到一起。

#### - 仓库(repository)

仓库是集中存放镜像文件的场所。仓库分为公开仓库（Public）和私有仓库（Private）两种形式。当用户创建了自己的镜像之后,可以使用 push 命令将它上传到公有或者私有仓库，这样下次在另外一台机器上使用这个镜像时候，只需要从仓库上 pull 下来就可以了。

#### - 容器(container)

Docker 利用容器（Container）来运行应用。容器是从镜像创建的运行实例。它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。可以把容器看做是一个简易版的 Linux 环境（包括 root 用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。因为一个容器就是一个完整的操作系统,所以可以实现 Run anywhere 的效果。容器实际上就是在镜像的最上层加上一层可读写层。

#### - 网络(network)

在 Docker 中，实现了强大的网络功能，我们不但能够十分轻松的对每个容器的网络进行配置，还能在容器间建立虚拟网络，将数个容器包裹其中，同时与其他网络环境隔离。

#### - 数据卷(volume)

基于 Docker 底层的 Union File System 技术。在 UnionFS 的加持下，除了能够从宿主操作系统中挂载目录外，还能够建立独立的目录持久存放数据，或者在容器间共享。

### Docker 安装部署

Docker 安装非常简单,windows 系统可以直接从官网下载 exe 安装包,linux 系统也可以通过添加 repo 然后使用 apt/yum 直接安装,具体步骤可以百度。

> ps：对于 windows 系统,新版的 Docker for windows 需要启用 Hyper-v,而旧版的 Docker ToolBox 依赖 VM VitualBox,如果使用旧版的安装,系统又启用了 hyper-v,则需要手动在创建 Docker machine 时指定使用 hyper-v 还是 VM VitualBox。

### Docker 常用命令

#### 获取镜像

```shell
$ docker pull
```

从仓库获取所需要的镜像。

使用示例：

```shell
$ docker pull hello-world
```

拉取镜像时,如果没有指明 registry,则默认从 Docker Hub 拉取;如果没有指定所有者,默认使用 official;如果没有指定 tag,默认使用 latest。

> 因为 Docker Hub 镜像仓库在国外的原因,拉取镜像会很慢,推荐使用阿里云镜像加速,具体使用参照阿里云文档: [容器镜像服务-镜像加速器](https://cr.console.aliyun.com/cn-shenzhen/instances/mirrors) .

#### 查看镜像列表

```shell
docker images
```

列出所有已经下载到 server 的镜像

使用示例：

```shell
$ docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
centos                   centos6             6a77ab6655b9        8 weeks ago         194.6 MB
ubuntu                   latest              2fa927b5cdd3        9 weeks ago         122 MB
```

在列出信息中，可以看到几个字段信息

- 来自于哪个仓库，比如 ubuntu
- 镜像的标记，比如 14.04
- 它的 ID 号（唯一）
- 创建时间
- 镜像大小

#### 构建镜像

```shell
docker build
```

使用 Dockerfile 来构建一个镜像,Dockerfile 相当于一个说明文档,告诉 Docker 应该如何构建镜像.

Dockerfile 示例

```shell
#初始镜像
FROM golang:1.12.1 AS build
#指定工作目录
WORKDIR /home/app/k8s-demo
#添加文件到镜像
ADD . .
#执行命令
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -mod=vendor .
#启动时执行命令
CMD ["./k8s-demo"]
```

更详细的语法说明请参考 [Dockerfile](https://docs.docker.com/engine/reference/builder/)

编写完 Dockerfile 后可以使用`docker build`来构建镜像

```shell
docker build -t sivdead/k8s-demo:lastet
```

#### 运行容器

```shell
docker run
```

从指定镜像创建容器

部署 docker 后,可以使用以下命令来判断是否部署成功

```shell
docker run hello-world
```

正常情况应该输出

```shell
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Already exists
Digest: sha256:0e11c388b664df8a27a901dce21eb89f11d8292f7fca1b3e3c4321bf7897bffe
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
```

#### 上传镜像

```shell
docker push
```

用户可以通过 docker push 命令，把自己创建的镜像上传到仓库中来共享。例如，用户在 Docker Hub 上完成注册后，可以推送自己的镜像到仓库中。

运行实例：

```shell
docker push sivdead/k8s-demo:lastet
```

#### 查看运行中的容器

```shell
docker ps
```

类似镜像,每一个容器都有一个唯一的 container id 标识.

#### 其他

所有 docker 命令可以使用`docker help`查看,也可以在[Docker 官方文档](https://docs.docker.com/v17.09/engine/reference/run/)上查看。

### Docker Compose

当需要启动多个容器,且多个容器之间需要通信时,可以在`docker run`参数中指定一个共同的`network`来实现,但这样比较不方便,这时候,可以使用 docker compose 来同时启动多个容器.

Docker Compose 是一个简单的 Docker 容器的编排工具，通过 YAML 文件配置需要运行的应用，然后通过 compose up 命令启动多个服务对应的容器实例。现版本的 Docker 中默认集成了 Compose,不需要另外安装。

docker-compose.yaml 示例：

```yaml
version: "3"
services:
  k8s-demo:
    image: sivdead/k8s-demo:0.0.3
    ports:
      - 8081:8081
    environment:
      REDIS_HOST: k8s-demo-redis
      REDIS_PORT: 6379
      REDIS_PASSWORD: 123456
    networks:
      - k8s-demo
    depends_on:
      - k8s-demo-redis
  k8s-demo-redis:
    image: redis:4.0
    networks:
      - k8s-demo
    command: redis-server --requirepass 123456
networks:
  k8s-demo:
```

上图中指定了两个镜像 k8s-dmeo 和 redis,使用同一个 network:k8s-demo。

启动:

```shell
docker-compose up -d
```

其中`-d` 用来使其在后台启动

停止:

```shell
docker-compose down
```

Docker compose 配置文件具体编写规则可以参考[官网](https://docs.docker.com/v17.09/compose/compose-file/).

### Kubernetes

Kubernetes 是 Google 开源的容器集群管理系统，使用 Go 语言实现，其提供应用部署、维护、 扩展机制等功能。目前可以在 GCE、vShpere、CoreOS、OpenShift、Azure 等平台使用 k8s。

国内目前 Aliyun 也提供了基于 k8s 的服务治理平台。如果是基于物理机、虚拟机搭建的 Docker 集群的话，也可以直接部署、运行 k8s。在微服务的集群环境下，Kubernetes 可以很方便管理跨机器的微服务容器实例。

### 为什么需要 Kubernetes

真实的生产环境应用会包含多个容器，而这些容器还很可能会跨越多个服务器主机部署。使用 Kubernetes，可以快速精准地部署应用程序，进行即时伸缩、灰度发布。

### Kubernetes 能做什么

目前 k8s 基本是公认的最强大开源服务治理技术之一。其主要提供以下功能：

- 自动化地基于 Docker 或其他容器服务(runc/Containerd 等)对服务实例进行部署和复制
- 以集群的方式运行，可以管理跨机器的容器，以及滚动升级、存储编排。
- 内置了基于 Docker 的服务发现和负载均衡模块
- K8s 提供了强大的自我修复机制,会对崩溃的容器进行替换(对用户，甚至开发团队都无感知)，并可随时扩容、缩容。让容器管理更加弹性化。

### Kubernetes 架构

Kubernetes 整体上遵循 C/S 架构,CLI 即 kubectl 命令行工具,CLI 通过 REST API 与 Server 进行通信。

```shell

                               +-------------+
                               |             |
                               |             |               +---------------+
                               |             |       +-----> |     Node 1    |
                               | Kubernetes  |       |       +---------------+
+-----------------+            |   Server    |       |
|       CLI       |            |             |       |       +---------------+
|    (Kubectl)    |----------->| ( Master )  |<------+-----> |     Node 2    |
|                 |            |             |       |       +---------------+
+-----------------+            |             |       |
                               |             |       |       +---------------+
                               |             |       +-----> |     Node 3    |
                               |             |               +---------------+
                               +-------------+
```

其中 server 架构如下

{% asset_img  k8s结构.png k8s结构  %}

#### - Master

- ETCD: 存储集群所有需持久化的状态，并且提供 watch 的功能支持，可以快速的通知各组件的变更等操作
- API Server: 接收外部的信号和请求，并将一些信息写入到 etcd 中。
- Controller Manager: 在后台运行着许多不同的控制器进程，用来调节集群的状态。
- Scheduler: Scheduler 是集群的调度器，它会持续的关注集群中未被调度的 Pod ，并根据各种条件，比如资源的可用性，节点的亲和性或者其他的一些限制条件，通过绑定的 API 将 Pod 调度/绑定到 Node 上。

#### - Node

Node 是 Kubernetes 集群架构中运行 Pod 的服务节点，用来承载被分配 Pod 的运行，是 Pod 运行的宿主机

- Kubelet: 负责管控容器，Kubelet 会从 Kubernetes API Server 接收 Pod 的创建请求，启动和停止容器，监控容器运行状态并汇报给 Kubernetes API Server。
- Container Runtime: 容器运行时最主要的功能是下载镜像和运行容器，我们最常见的实现可能是 Docker , 目前还有其他的一些实现，比如 runc, Containered。
  K8S 提供了一套通用的容器运行时接口 CRI (Container Runtime Interface), 凡是符合这套标准的容器运行时实现，均可在 K8S 上使用。
- Kube Proxy
  负责为 Pod 创建代理服务，KubeProxy 会从 API Server 获取所有的 Service 信息，并根据 Service 的信息创建代理服务，实现 Service 到 Pod 的请求路由和转发。

### Kubernetes 核心概念

#### - Namespace

Namespace 是对一组资源和对象的抽象集合，比如可以用来将系统内部的对象划分为不同的项目组或用户组。常见的 pods, services, replication controllers 和 deployments 等都是属于某一个 namespace 的（默认是 default），而 node, persistentVolumes 等则不属于任何 namespace。

Namespace 常用来隔离不同的用户，比如 Kubernetes 自带的服务一般运行在 kube-system namespace 中。

Namespace 定义实例:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: demo
```

> kubectl 可以通过–namespace 或者-n 选项指定 namespace。如果不指定，默认为 default。查看操作下,也可以通过设置–all-namespace=true 来查看所有 namespace 下的资源。

#### - Pod

在 Kubernetes 中，最小的管理元素不是一个个独立的容器，而是 Pod,Pod 是最小的，管理，创建，计划的最小单元。一个 Pod 是一个容器环境下的“逻辑主机”，它可能包含一个或者多个紧密相连并且共享磁盘的容器。

Pod 定义文件示例:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    app: k8s-demo
  name: k8s-demo-app
  namespace: demo
spec:
  #容器列表
  containers:
    - image: sivdead/k8s-demo:0.0.8
      imagePullPolicy: Always
      name: k8s-demo
      ports:
        - containerPort: 8081
      env:
        - name: REDIS_HOST
          value: "k8s-demo-redis"
        - name: REDIS_PORT
          value: "6379"
        - name: REDIS_PASSWORD
          value: "2JmUPwEf2W"
```

#### - Label

标签其实就一对 key/value ，被关联到资源上，比如 Pod,标签可以用来划分特定组的对象（比如，所有女的），标签可以在创建一个对象的时候直接给与，也可以在后期随时修改，每一个对象可以拥有多个标签，但是，key 值必须是唯一的。

#### - Label Selector

通过 Label Selector，客户端/用户能方便辨识出一组对象。Label Selector 是 kubernetes 中核心的组织原语。

API 目前支持两种选择器：基于相等的和基于集合的。一个 Label Selector 一可以由多个必须条件组成，由逗号分隔。在多个必须条件指定的情况下，所有的条件都必须满足，因而逗号起着 AND 逻辑运算符的作用。

#### - Replication Controller

Replication Controller( 简称 RC )是 Kubernetes 系统中的核心概念之一,简单来说，它其实是定义了一个期望的场景,即声明某种 Pod 的副本数量在任意时刻都符合某个预期值,所以 RC 的定义包括如下几个部分:

- Pod 期待的副本数(replicas).
- 用于筛选目标 Pod 的 Label Selector.
- 当 Pod 的副本数量小于预期数量时,用于创建新 Pod 的 Pod 模板(template).

ReplicaSet 是下一个版本的 RC,它和 RC 的唯一区别是: ReplicaSet 支持基于集合的 Label Selector,当前我们很少单独使用 ReplicaSet,它主要被 Deployment 这个更高层的资源对象所使用.

RC 定义文件示例:

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: k8s-demo
spec:
  replicas: 2
  selector:
    app: k8s-demo
  template:
    metadata:
      #标签选择器
      labels:
        app: k8s-demo
    spec:
      containers:
        - image: sivdead/k8s-demo:0.0.8
          imagePullPolicy: Always
          name: k8s-demo
          ports:
            - containerPort: 8081
          env:
            - name: REDIS_HOST
              value: "k8s-demo-redis"
            - name: REDIS_PORT
              value: "6379"
            - name: REDIS_PASSWORD
              value: "2JmUPwEf2W"
```

#### - Deployment

Deployment 为 Pod 和 ReplicaSet 提供了一个声明式定义(declarative)方法，用来替代以前的 ReplicationController 来方便的管理应用。典型的应用场景包括：

- 定义 Deployment 来创建 Pod 和 ReplicaSet
- 滚动升级和回滚应用
- 扩容和缩容
- 暂停和继续 Deployment

Deployment 定义文件示例:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: k8s-demo
  name: k8s-demo-app
  namespace: demo
spec:
  selector:
    matchLabels:
      app: k8s-demo
  template:
    metadata:
      labels:
        app: k8s-demo
    spec:
      containers:
        - image: sivdead/k8s-demo:0.0.8
          imagePullPolicy: Always
          name: k8s-demo
          ports:
            - containerPort: 8081
          env:
            - name: REDIS_HOST
              value: "k8s-demo-redis"
            - name: REDIS_PORT
              value: "6379"
            - name: REDIS_PASSWORD
              value: "2JmUPwEf2W"
```

#### - Horizontal Pod Autoscaling

Horizontal Pod Autoscaling 可以根据 CPU 使用率或应用自定义 metrics 自动扩展 Pod 数量（支持 replication controller、deployment 和 replica set）。

- 控制管理器每隔 30s（可以通过–horizontal-pod-autoscaler-sync-period 修改）查询 metrics 的资源使用情况
- 支持三种 metrics 类型
  - 预定义 metrics（比如 Pod 的 CPU）以利用率的方式计算
  - 自定义的 Pod metrics，以原始值（raw value）的方式计算
  - 自定义的 object metrics
- 支持两种 metrics 查询方式：Heapster 和自定义的 REST API
- 支持多 metrics

HPA 定义文件示例:

```yaml
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: k8s-demo
  namespace: demo
spec:
  maxReplicas: 10
  minReplicas: 1
  #自动扩容资源对象
  scaleTargetRef:
    kind: Deployment
    name: k8s-demo
  #扩容的cpu使用率阀值
  targetCPUUtilizationPercentage: 90
```

#### - Service

Kubernete Service 是一个定义了一组 Pod 的策略的抽象,Service 通过 Label Selector 来关联到一组 Pod,并将这些 Pod 的特定端口暴露出去,这种暴露可以是 ClusterIP 或 NodePort。

- NodePort: 使用这种方式暴露的 Service,可以直接使用 NodeIP:NodePort 来访问。
- ClusterIP: ClusterIP 是一个虚拟的 ip 地址,只在集群内可以访问,这种一般是用负载均衡服务来作转发。

Service 定义文件示例:

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: k8s-demo
  name: k8s-demo-app
  namespace: demo
spec:
  selector:
    app: k8s-demo
  ports:
    - port: 8081
      protocol: TCP
      targetPort: 8081
  type: ClusterIP
```

#### - Secret

Secret 解决了密码、token、密钥等敏感数据的配置问题，而不需要把这些敏感数据暴露到镜像或者 Pod Spec 中。Secret 可以以 Volume 或者环境变量的方式使用。

Secret 有三种类型：

- Service Account：用来访问 Kubernetes API，由 Kubernetes 自动创建，并且会自动挂载到 Pod 的/run/secrets/kubernetes.io/serviceaccount 目录中；
- Opaque：base64 编码格式的 Secret，用来存储密码、密钥等；
- kubernetes.io/dockerconfigjson: 用来存储私有 docker registry 的认证信息。

#### - Ingress

Ingress 是一组允许外部请求进入集群的路由规则的集合。它可以给 Service 提供集群外部访问的 URL，负载均衡，SSL 终止等。

直白点说，Ingress 就类似起到了智能路由的角色，外部流量到达 Ingress ，再由它按已经制定好的规则分发到不同的后端服务中去。

Ingress 可以有多种控制器（实现）,目前由官方维护的有两个: 适用于 Google Cloud 的 [GLBC](https://github.com/kubernetes/ingress-gce)，当你使用 GKE 的时候，便会看到它；和 [NGINX Ingress Controller](https://github.com/kubernetes/ingress-nginx)，它是使用 ConfigMap 存储 Nginx 配置实现的。

Ingress 并不是 Kubernetes 自带的,需要自己手动安装。以下说明一下 NGINX Ingress Controller 的安装步骤:

> 所有步骤皆为按配置文件创建资源,所以我只列了配置文件,安装时依次使用`kubectl apply -f filename`安装即可。
> 以下配置文件全部来自[官方文档](https://kubernetes.github.io/ingress-nginx/deploy/),但是现在官方文档上改了,没有这个配置文件了,所以我把我保存的发出来.

#### 1. 创建 Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
```

#### 2. 创建 configMap(nginx 配置文件)

```yaml
kind: ConfigMap
apiVersion: v1
metadata:
  name: nginx-configuration
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
---
kind: ConfigMap
apiVersion: v1
metadata:
  name: tcp-services
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
---
kind: ConfigMap
apiVersion: v1
metadata:
  name: udp-services
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
```

#### 3. 创建帐号、角色及角色绑定

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: nginx-ingress-serviceaccount
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: nginx-ingress-clusterrole
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
rules:
  - apiGroups:
      - ""
    resources:
      - configmaps
      - endpoints
      - nodes
      - pods
      - secrets
    verbs:
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - nodes
    verbs:
      - get
  - apiGroups:
      - ""
    resources:
      - services
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - "extensions"
    resources:
      - ingresses
    verbs:
      - get
      - list
      - watch
  - apiGroups:
      - ""
    resources:
      - events
    verbs:
      - create
      - patch
  - apiGroups:
      - "extensions"
    resources:
      - ingresses/status
    verbs:
      - update
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: Role
metadata:
  name: nginx-ingress-role
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
rules:
  - apiGroups:
      - ""
    resources:
      - configmaps
      - pods
      - secrets
      - namespaces
    verbs:
      - get
  - apiGroups:
      - ""
    resources:
      - configmaps
    resourceNames:
      # Defaults to "<election-id>-<ingress-class>"
      # Here: "<ingress-controller-leader>-<nginx>"
      # This has to be adapted if you change either parameter
      # when launching the nginx-ingress-controller.
      - "ingress-controller-leader-nginx"
    verbs:
      - get
      - update
  - apiGroups:
      - ""
    resources:
      - configmaps
    verbs:
      - create
  - apiGroups:
      - ""
    resources:
      - endpoints
    verbs:
      - get
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: RoleBinding
metadata:
  name: nginx-ingress-role-nisa-binding
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: nginx-ingress-role
subjects:
  - kind: ServiceAccount
    name: nginx-ingress-serviceaccount
    namespace: ingress-nginx
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: nginx-ingress-clusterrole-nisa-binding
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: nginx-ingress-clusterrole
subjects:
  - kind: ServiceAccount
    name: nginx-ingress-serviceaccount
    namespace: ingress-nginx
```

#### 4. 创建 nginx-ingress-controller

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-ingress-controller
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app.kubernetes.io/name: ingress-nginx
      app.kubernetes.io/part-of: ingress-nginx
  template:
    metadata:
      labels:
        app.kubernetes.io/name: ingress-nginx
        app.kubernetes.io/part-of: ingress-nginx
      annotations:
        prometheus.io/port: "10254"
        prometheus.io/scrape: "true"
    spec:
      serviceAccountName: nginx-ingress-serviceaccount
      containers:
        - name: nginx-ingress-controller
          image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.24.1
          args:
            - /nginx-ingress-controller
            - --configmap=$(POD_NAMESPACE)/nginx-configuration
            - --tcp-services-configmap=$(POD_NAMESPACE)/tcp-services
            - --udp-services-configmap=$(POD_NAMESPACE)/udp-services
            - --publish-service=$(POD_NAMESPACE)/ingress-nginx
            - --annotations-prefix=nginx.ingress.kubernetes.io
          securityContext:
            allowPrivilegeEscalation: true
            capabilities:
              drop:
                - ALL
              add:
                - NET_BIND_SERVICE
            # www-data -> 33
            runAsUser: 33
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: POD_NAMESPACE
              valueFrom:
                fieldRef:
                  fieldPath: metadata.namespace
          ports:
            - name: http
              containerPort: 80
            - name: https
              containerPort: 443
          livenessProbe:
            failureThreshold: 3
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            initialDelaySeconds: 10
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 10
          readinessProbe:
            failureThreshold: 3
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 10
```

#### 5. 暴露 Ingress Controller 服务

Ingress 的作用在于将集群外的请求流量转向集群内的服务，而默认情况下,集群外和集群内是不互通的，所以必须将 NGINX Ingress Controller 暴露至集群外，以便让其能接受来自集群外的请求,这里使用 NodePort 的方式暴露。

```yaml
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: NodePort
  ports:
    - name: http
      port: 80
      targetPort: 80
      protocol: TCP
    - name: https
      port: 443
      targetPort: 443
      protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
```

创建 service 之后,即可使用 NodeIp:NodePort,根据定义的路由规则访问其他服务。

Ingress 定义文件示例:

```yaml
# 最新版的k8s使用的Ingress的apiVersion为networking.k8s.io/v1beta1
# 这里用的是阿里云镜像服务可用的apiVersion
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: k8s-demo-ingress
  namespace: demo
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  rules:
    - http:
        paths:
          - path: /k8s-demo/(.*)
            backend:
              # 关联的Service名称
              serviceName: "k8s-demo-app"
              servicePort: 8081
      # 绑定的域名,创建后可以修改host文件来使用这个域名访问服务
      host: sivded.com
```

### Kubernetes 安装部署

#### - 本地环境搭建

本地环境搭建简易可行的可选方式有两种:Kind 和 Minikube,这里推荐使用 Kind.

Kind 是 Kubernetes In Docker 的缩写，顾名思义是使用 Docker 容器作为 Node 并将 Kubernetes 部署至其中的一个工具。官方文档中也把 Kind 作为一种本地集群搭建的工具进行推荐。

##### Kind 安装

Kind 使用 Golang 进行开发，在仓库的 [Release](hhttps://github.com/kubernetes-sigs/kind/releases) 页面，已经上传了构建好的二进制，支持多种操作系统，可直接按需下载进行使用。

示例:

```shell
# 下载最新的 0.3.0 版本
wget -O /usr/local/bin/kind https://github.com/kubernetes-sigs/kind/releases/download/0.2.0/kind-linux-amd64 && chmod +x /usr/local/bin/kind
```

##### 依赖

- Kind 的主要功能目前需要有 Docker 环境的支持。
- 如果需要操作集群，则需要安装 kubectl 命令行。安装方法可参考[官方文档](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl).

##### 使用

```shell
# --name指定cluster名称,如果不指定则为默认"kind"
➜  ~ skind create cluster --name sivdead
Creating cluster "sivdead" ...
 ✓ Ensuring node image (kindest/node:v1.14.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Creating kubeadm config 📜
 ✓ Starting control-plane 🕹️
Cluster creation complete. You can now use the cluster with:

export KUBECONFIG="$(kind get kubeconfig-path --name="sivdead")"
kubectl cluster-info
```

命令中的输出让我们使用`export KUBECONFIG="$(kind get kubeconfig-path --name="sivdead")"`来配置 kubectl 环境变量,但这种方式只在当前窗口有效,实际可以修改`/etc/profile`来使配置永久生效.

```shell
#kube config
KUBECONFIG=`kind get kubeconfig-path --name='sivdead'`
#添加KUBECONFIG环境变量
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL KUBECONFIG
```

修改完成后 source 一下即可使用 kubectl 获取集群信息

```shell
➜  ~ source /etc/profile
➜  ~ kubectl cluster-info
Kubernetes master is running at https://localhost:45560
KubeDNS is running at https://localhost:45560/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

```

可以看到单节点的 Kubernetes 已经搭建成功.

这时候使用`docker ps`,也可以看到对应的 Node 容器正在运行.

```shell
➜  ~ docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                                  NAMES
1a69bb53e1b3        kindest/node:v1.14.2   "/usr/local/bin/entr…"   13 days ago         Up 13 days          45560/tcp, 127.0.0.1:45560->6443/tcp   kind-control-plane

```

在 kind 拉取 Kubernetes 相关镜像时,可能会因为镜像源被墙导致拉取不到镜像报错.这时我们可以使用配置文件的方式来指定使用国内镜像.

首先删除刚才报错的镜像

```shell
➜  ~ kind delete  cluster --name  sivdead
Deleting cluster "sivdead" ...
$KUBECONFIG is still set to use /root/.kube/kind-config-sivdead even though that file has been deleted, remember to unset it
```

然后创建`kind-config.yaml`

```yaml
kind: Cluster
apiVersion: kind.sigs.k8s.io/v1alpha3
kubeadmConfigPatches:
  - |
    apiVersion: kubeadm.k8s.io/v1beta1
    kind: ClusterConfiguration
    metadata:
      name: config
    networking:
      serviceSubnet: 10.0.0.0/16
    imageRepository: registry.aliyuncs.com/google_containers
    nodeRegistration:
      kubeletExtraArgs:
        pod-infra-container-image: registry.aliyuncs.com/google_containers/pause:3.1
  - |
    apiVersion: kubeadm.k8s.io/v1beta1
    kind: InitConfiguration
    metadata:
      name: config
    networking:
      serviceSubnet: 10.0.0.0/16
    imageRepository: registry.aliyuncs.com/google_containers
nodes:
  - role: control-plane
```

使用该配置文件搭建集群:

```shell script
➜  ~  kind create cluster --name sivdead --config-kind.yaml
Creating cluster "sivdead" ...
 ✓ Ensuring node image (kindest/node:v1.14.2) 🖼
 ✓ Preparing nodes 📦
 ✓ Creating kubeadm config 📜
 ✓ Starting control-plane 🕹️
Cluster creation complete. You can now use the cluster with:

export KUBECONFIG="$(kind get kubeconfig-path --name="sivdead")"
kubectl cluster-info
```

#### - 高可用集群搭建

高可用集群可以使用 Kind 或者 Kubeadm 来搭建,具体可以参考:

- [使用 Kind 搭建你的本地 Kubernetes 集群](https://zhuanlan.zhihu.com/p/60464867?utm_source=wechat_session&utm_medium=social&utm_oi=31223179116544)
- [kubernetes v1.14.0 高可用 master 集群部署(使用 kubeadm)](https://www.kubernetes.org.cn/5273.html)

### kubectl 常用命令

kubectl 命令行的语法如下:

```shell
kubectl [command] [TYPE] [NAME] [flags]
```

- command: 子命令,用于操作集群资源对象的命令,常用命令:

  - create: 创建资源对象
  - apply: 从配置文件或 stdin 中对资源对象进行配置更新,也可以用于创建资源对象
  - scale: 扩容/缩容一个 Deployment、ReplicaSet、RC 或 Job 中 Pod 的数量,可以将 Pod 数量设置为 0 来达到暂时停止应用的目的.
  - delete: 删除资源对象,可通过-f=filename 以配置文件格式指定删除的内容
  - describe: 描述资源对象,describe 在排查错误时非常有用
  - get: 查看资源对象,可以使用`--watch`来动态查看资源对象列表
  - exec: 执行容器的命令,通常可以使用下列命令来进入到某个 pod 容器的 bash 命令行.

    ```shell
    # -c 指定容器名称,如果不指定,则默认使用pod中的第一个容器
    kubectl exec -it podName -c containerName /bin/bash
    ```

  - logs: 查看容器的日志,参数`-f`可以达到类似`tailf`的效果
  - cp: 从容器中复制文件,要求容器中可以使用`tar`命令,用法:

    ```shell
    kubectl cp <namespace>/<pod>:<src-filepath> <namespace>/<pod>:<dest-filepath> [options]
    ```

- TYPE: 资源对象的类型,区分大小写,能以单数形式、复数形式、简写形式表示.例如下列 3 种 TYPE 是等价的.

```shell
kubectl get pod
kubectl get pods
kubectl get po
```

&emsp;常用资源对象及其简写如下:

| 资源对象名称          | 简写   |
| --------------------- | ------ |
| configmap             | cm     |
| deployment            | deploy |
| ingress               | ing    |
| node                  | no     |
| namespace             | ns     |
| pod                   | po     |
| replicationcontroller | rc     |
| replicaset            | rs     |
| service               | svc    |

- NAME: 资源对象的名称,区分大小写.如果不指定名称,则系统将返回属于 TYPE 的全部对象的列表,例如`kubectl get pod`将返回所有 pod 的列表
- flags: kubectl 子命令的可选参数,例如使用`-n`指定 Namespace.常用参数:
  - `-n`: 指定 Namespace,如果不指定则使用 default
  - `-o`: 指定输出格式,可以将输出格式修改为 yaml 或者 json 等格式,也可以指定返回的字段。

### Quick Start: 使用 Kubernetes 发布应用

我们使用之前编写的简单计数应用镜像。

首先,编写配置文件:

- Namespace:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: demo
```

- Deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: k8s-demo
  name: k8s-demo-app
  namespace: demo
spec:
  selector:
    matchLabels:
      app: k8s-demo
  template:
    metadata:
      labels:
        app: k8s-demo
    spec:
      containers:
        - image: sivdead/k8s-demo:0.0.1
          imagePullPolicy: Always
          name: k8s-demo
          ports:
            - containerPort: 8081
          env:
            - name: REDIS_HOST
              value: "k8s-demo-redis"
            - name: REDIS_PORT
              value: "6379"
            - name: REDIS_PASSWORD
              value: "123456"
```

- Service:

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: k8s-demo
  name: k8s-demo-app
  namespace: demo
spec:
  selector:
    app: k8s-demo
  ports:
    - port: 8081
      protocol: TCP
      targetPort: 8081
  type: ClusterIP
```

- Ingress

```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: k8s-demo-ingress
  namespace: demo
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$1
spec:
  rules:
    - http:
        paths:
          - path: /k8s-demo/(.*)
            backend:
              serviceName: "k8s-demo-app"
              servicePort: 8081
      host: sivdead.com
```

- Redis Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: redis
  name: k8s-demo-redis
  namespace: demo
spec:
  selector:
    matchLabels:
      app: redis
  replicas: 1
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
        - image: redis:4.0
          name: redis
          ports:
            - containerPort: 6379
          args:
            - '--requirepass 123456'
```

- Redis Service

因为 redis 不需要被集群外部使用,所以使用 ClusterIP 即可

```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: redis
  name: k8s-demo-redis
  namespace: demo
spec:
  ports:
    - port: 6379
      protocol: TCP
      targetPort: 6379
  selector:
    app: redis
  type: ClusterIP
```

使用`kubectl apply -f`轮流创建资源后,修改`/etc/hosts`文件,增加`sivdead.com`对应`NGINX Ingress Controller`的`NodeIP:NodePort`

```shell
➜  ~ kubectl -n ingress-nginx get svc
NAME            TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
ingress-nginx   NodePort   10.105.250.114   <none>        80:31895/TCP,443:31693/TCP   2d13h

➜  ~ kubectl describe node kind-control-plane
Name:               kind-control-plane
# 忽略...
Addresses:
  InternalIP:  172.17.0.2
  Hostname:    kind-control-plane
# 忽略...

➜  ~ cat >>/etc/hosts<<EOF
heredoc> 172.17.0.2   sivdead.com
heredoc> EOF

```

查看 demo Namespace 各资源的状态

```shell
➜  ~ kubectl -n demo get all
NAME                                  READY   STATUS    RESTARTS   AGE
pod/k8s-demo-app-696b78444b-vn2kj     1/1     Running   3          2d22h
pod/k8s-demo-redis-7cf684b8ff-grlx6   1/1     Running   1          2d22h

NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
service/k8s-demo-app     ClusterIP   10.107.18.40    <none>        8081/TCP         2d13h
service/k8s-demo-redis   NodePort    10.104.21.255   <none>        6379:32201/TCP   2d22h

NAME                             READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/k8s-demo-app     1/1     1            1           2d22h
deployment.apps/k8s-demo-redis   1/1     1            1           2d22h

NAME                                        DESIRED   CURRENT   READY   AGE
replicaset.apps/k8s-demo-app-696b78444b     1         1         1       2d22h
replicaset.apps/k8s-demo-app-854b97479d     0         0         0       2d22h
replicaset.apps/k8s-demo-redis-7cf684b8ff   1         1         1       2d22h

```

如果所有资源都在正常运行,使用 curl 测试接口:

```shell
➜  ~ curl sivdead.com:31895/k8s-demo/score
score is: 10#
```

说明应用已经部署成功。

### 引用

> - 掘金小册[《Kubernetes 从上手到实践-张晋涛》](https://juejin.im/book/5b9b2dc86fb9a05d0f16c8ac)
> - 电子工业出版社《Kubernetes 权威指南》
