[TOC]



---



# 一、Docker简介

## 1、前提知识

1.1 强制，熟悉Linux命令和相关背景知识 ps top

1.2 建议，Git相关知识 git pull

## 2、课程时间

1.5天。

## 3、课程定位和范围

立足JavaEE。

## 4、Docker是什么

### 4.1 问什么会有Docker出现

> 一款产品从开发到上线，从操作系统，到运行环境，再到应用配置。作为开发+运维之间的协作我们需要关心很多东西，这也是很多互联网公司都不得不面对的问题，特别是各种版本的迭代之后，不同版本环境的兼容，对运维人员都是考验。
>
> Docker之所以发展如此迅速，也是因为它对此给出了一个标准化的解决方案。
>
> 环境配置如此麻烦，换一台机器，就要重来一次，费时费力。很多人想到，能不能从根本上解决问题，软件可以带环境安装？也就是说，安装的时候，把原始环境一模一样地复制过来。开发人员利用Docker可以消除协作编码时“在我的机器上可以正常工作，但是换一个机器就不能正常工作”的问题。
>

![Docker镜像技术](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E9%95%9C%E5%83%8F%E6%8A%80%E6%9C%AF.png)

> 之前在服务器配置一个应用的运行环境，要安装各种软件，就拿尚硅谷电商项目的环境来说吧，Java/Tomcat/MySQL/JDBC驱动包等。安装和配置这些东西有多麻烦就不说了，它还不能跨平台。假如我们是在Windows 上安装的这些环境，到了Linux又得重新装。况且就算不跨操作系统，换另一台同样操作系统的服务器，要移植应用也是非常麻烦的。
>
> 传统上认为，软件编码开发/测试结束后，所产出的成果即是程序或是能够编译执行的二进制字节码等(java为例)。 而为了让这些程序可以顺利执行，开发团队也得准备完整的部署文件，让维运团队得以部署应用程式，开发需要清楚的告诉运维部署团队，用的全部配置文件+所有软件环境。不过，即便如此，仍然常常发生部署失败的状况。Docker镜像的设计，使得Docker得以打破过去「程序即应用」的观念。透过镜像(images)将作业系统核心除外，运作应用程式所需要的系统环境，由下而上打包，达到应用程式跨平台间的无缝接轨运作。
>

### 4.2 Docker理念

> Docker是基于Go语言实现的云开源项目。
>
> Docker的主要目标是“Build，Ship and Run Any App，Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行环境能够做到“一次封装，到处运行”。
>

![Docker理念](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E7%90%86%E5%BF%B5.png)

> Linux容器技术的出现就解决了这样一个问题，而Docker就是在它的基础上发展过来的。将应用运行在Docker容器上面，而Docker容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一键部署好，大大简化了操作。
>

### 4.3 一句话

> 解决了运行环境和配置问题软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术。

## 5、Docker能干嘛

### 5.1 之前的虚拟机技术

> 虚拟机(virtual machine)就是带环境安装的一种解决方案。
>
> 它可以在一种操作系统里面运行另一种操作系统，比如在Windows系统里面运行Linux系统。应用程序对此毫无感知，因为虚拟机看上去跟真实系统一模一样，而对于底层系统来说，虚拟机就是一个普通文件，不需要了就删掉，对其他部分毫无影响。这类虚拟机完美的运行了另一套系统，能够使应用程序，操作系统和硬件三者之间的逻辑不变。
>

![之前的虚拟机技术](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E4%B9%8B%E5%89%8D%E7%9A%84%E8%99%9A%E6%8B%9F%E6%9C%BA%E6%8A%80%E6%9C%AF.png)

> 虚拟机的缺点：①资源占用多；②冗余步骤多；③启动慢
>

### 5.2 容器虚拟化技术

> 由于前面虚拟机存在这些缺点，Linux 发展出了另一种虚拟化技术：Linux 容器(Linux Containers，缩写为LXC)。
>
> **Linux容器不是模拟一个完整的操作系统**，而是对进程进行隔离。有了容器，就可以将软件运行所需的所有资源打包到一个隔离的容器中。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的库资源和设置。系统因此而变得高效轻量并保证部署在任何环境中的软件都能始终如一地运行。

![容器虚拟化技术](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E5%AE%B9%E5%99%A8%E8%99%9A%E6%8B%9F%E5%8C%96%E6%8A%80%E6%9C%AF.png)

> 比较Docker和传统虚拟化方式的不同之处：
>
> - 传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整的操作系统，在该系统上再运行所需应用进程。
> - 而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，**而且也没有进行硬件虚拟**。因此容器要比传统虚拟机更为轻便。
> - 每个容器之间互相隔离，每个容器有自己的文件系统，容器之间进程不会相互影响，能区分计算资源。
>

### 5.3 开发/运维（DevOps）

一次构建、随处运行。

#### 更快速的应用交付和部署

> 传统的应用开发完成后，需要提供一堆安装程序和配置说明文档，安装部署后需根据配置文档进行繁杂的配置才能正常运行。Docker化之后只需要交付少量容器镜像文件，在正式生产环境加载镜像并运行即可，应用安装配置在镜像里已经内置好，大大节省部署配置和测试验证时间。
>

#### 更便捷的升级和扩缩容

> 随着微服务架构和Docker的发展，大量的应用会通过微服务方式架构，应用的开发构建将变成搭乐高积木一样，每个Docker容器将变成一块“积木”，应用的升级将变得非常容易。当现有的容器不足以支撑业务处理时，可通过镜像运行新的容器进行快速扩容，使应用系统的扩容从原先的天级变成分钟级甚至秒级。
>

#### 更简单的系统运维

> 应用容器化运行后，生产环境运行的应用可与开发、测试环境的应用高度一致，容器会将应用程序相关的环境和状态完全封装起来，不会因为底层基础架构和操作系统的不一致性给应用带来影响，产生新的BUG。当出现程序异常时，也可以通过测试环境的相同容器进行快速定位和修复。
>

#### 更高效的计算资源利用

> **Docker是内核级虚拟化**，其不像传统的虚拟化技术一样需要额外的Hypervisor支持，所以在一台物理机上可以运行很多个容器实例，可大大提升物理服务器的CPU和内存的利用率。

## 6、Docker去哪下载

### 6.1 官网

> docker官网： https://www.docker.com/
>
> docker中文网站: https://www.docker-cn.com/
>

### 6.2 仓库

> Docker Hub官网：https://hub.docker.com/
>

---

# 二、Docker安装

## 1、前提说明

### 1.1 CentOS Docker安装

> Docker支持以下的CentOS版本：
>
> CentOS 7（64-bit）
>
> CentOS 6.5（64-bit）或更高版本
>

### 1.2 前提条件

> 目前，CentOS仅发行版本中的内核支持Docker。
>
> Docker运行在CentOS 7上，要求系统为64位、系统内核版本为3.10以上。
>
> Docker运行在CentOS 6.5或更高版本的CentOS上，要求系统为64位、系统内核版本为2.6.32-431或更高版本。
>

### 1.3 查看自己的内核

uname命令用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等）。

![Linux查看自己的内核](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Linux%E6%9F%A5%E7%9C%8B%E8%87%AA%E5%B7%B1%E7%9A%84%E5%86%85%E6%A0%B8.png)

### 1.4 查看已安装的CentOS版本信息

![查看已安装的CentOS版本信息](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E6%9F%A5%E7%9C%8B%E5%B7%B2%E5%AE%89%E8%A3%85%E7%9A%84CentOS%E7%89%88%E6%9C%AC%E4%BF%A1%E6%81%AF.png)

或者使用以下命令：

![查看已安装的CentOS版本信息2](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E6%9F%A5%E7%9C%8B%E5%B7%B2%E5%AE%89%E8%A3%85%E7%9A%84CentOS%E7%89%88%E6%9C%AC%E4%BF%A1%E6%81%AF2.png)

## 2、Docker的基本组成

### 2.1 Docker架构图

![Docker架构图](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

### 2.2 镜像（image）

> Docker镜像（Image）就是一个**只读**的模板。镜像可以用来创建Docker容器，**一个镜像可以创建很多容器**。
>

![Docker的容器与镜像类比Java](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E7%9A%84%E5%AE%B9%E5%99%A8%E4%B8%8E%E9%95%9C%E5%83%8F%E7%B1%BB%E6%AF%94Java.png)

### 2.3 容器（container）

> Docker利用容器？（Container）独立运行的一个或一组应用。**容器是用镜像创建的运行实例。**
>
> 它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台。
>
> **可以把容器看做是一个简易版的Linux环境**（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。
>
> 容器的定义和镜像几乎一模一样，也是一堆层的统一视角，唯一区别在于容器的最上面那一层是可读可写的。
>

### 2.4 仓库（repository）

> 仓库（Repository）是**集中存放镜像**文件的场所。
>
> 仓库（Repository）和仓库注册服务器（Registry）是有区别的。仓库注册服务器上往往存放着多个仓库，每个仓库中又包含了多镜像，每个镜像有不同的标签（tag）。
>
> 仓库分为公开仓库（Public）和私有仓库（Private）两种形式。**最大的公开仓库是Docker Hub(https://hub.docker.com/)** 存放了数量庞大的镜像供用户下载。国内的公开仓库包括阿里云、网易云等。
>

### 2.5 总结

> 需要正确的理解仓储/镜像/容器这几个概念:
>
> Docker本身是一个容器运行载体或称之为管理引擎。我们把应用程序和配置依赖打包好形成一个可交付的运行环境，这个打好的运行环境就是image镜像文件。只有通过这个镜像文件才能生成Docker容器。image文件可以看作是容器的模板。Docker根据image文件生成容器的实例。同一个image文件，可以生成多个同时运行的容器实例。
>
> - image文件生成的容器实例，本身也是一个文件，称为镜像文件。
>
> - 一个容器运行一种服务，当我们需要的时候，就可以通过docker客户端创建一个对应的运行实例，也就是我们的容器。
>
> - 至于仓储，就是放了一堆镜像的地方，我们可以把镜像发布到仓储中，需要的时候从仓储中拉下来就可以了。
>

## 3、安装步骤

### 3.1 CentOS 6.8安装Docker

> 1、yum install -y epel-release
>
> 2、yum install -y docker-io
>
> 3、安装后的配置文件：/etc/sysconfig/docker
>
> 4、启动Docker后台服务：service docker start
>
> 5、Docker Version验证

### 3.2 CentOS 7安装Docker

https://docs.docker.com/engine/install/centos/

## 4、永远的HelloWorld

### 4.1 阿里云镜像加速

登录自己的阿里云账号，在开发者控制台中可以找到容器镜像服务，获取自己的加速器地址链接。

#### 配置镜像加速器

针对Docker客户端版本大于 1.10.0 的用户

您可以通过修改daemon配置文件/etc/docker/daemon.json来使用加速器

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://6ivdbwy7.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

> 可能刚安装没有/etc/docker/daemon.json文件，手动创建并写入
>
> {
>   "registry-mirrors": ["https://6ivdbwy7.mirror.aliyuncs.com"]
> }

### 4.2 网易云等其他镜像加速

基本同阿里云步骤，镜像加速地址为

```
"registry-mirrors": ["https://hub-mirror.c.163.com"]

科大镜像：https://docker.mirrors.ustc.edu.cn/
网易：https://hub-mirror.c.163.com/
七牛云加速器：https://reg-mirror.qiniu.com
```

### 4.3 启动Docker后台容器测试运行hello-world

![Docker第一次执行hello-world](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E7%AC%AC%E4%B8%80%E6%AC%A1%E6%89%A7%E8%A1%8Chello-world.png)

### 4.4 docker run 干了什么

![Docker run干了什么](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%20run%E5%B9%B2%E4%BA%86%E4%BB%80%E4%B9%88.png)

## 5、底层原理

### 5.1 Docker是怎么工作的

> Docker是一个Client-Server结构的系统，Docker守护进程运行在主机上，然后通过Socket连接从客户端访问，守护进程从客户端接受命令并管理运行在主机上的容器。**容器，是一个运行时环境，就是我们前面说到的集装箱。**
>

### 5.2 为什么Docker比VM快

- docker有着比虚拟机更少的抽象层。由于docker不需要Hypervisor实现硬件资源虚拟化，运行在docker容器上的程序直接使用的都是实际物理机的硬件资源。因此在CPU、内存利用率上docker将会在效率上有明显优势。

- docker利用的是宿主机的内核，而不需要Guest OS。因此，当新建一个 容器时，docker不需要和虚拟机一样重新加载一个操作系统内核仍而避免引寻、加载操作系统内核返个比较费时费资源的过程，当新建一个虚拟机时，虚拟机软件需要加载GuestOS，返个新建过程是分钟级别的。而docker由于直接利用宿主机的操作系统，则省略了返个过程，因此新建一个docker容器只需要几秒钟。

![Docker和VM比较](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E5%92%8CVM%E6%AF%94%E8%BE%83.png)

---

# 三、Docker常用命令

## 1、帮助命令

```shell
docker version

docker info

docker --help
```

## 2、镜像命令

### 2.1 docker images

列出本地主机上的镜像

![Docker images命令](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%20images%E5%91%BD%E4%BB%A4.png)

```
OPTIONS说明
-a：列出本地所有的镜像（含中间映像层）
-q：只显示镜像ID
--digests：显示镜像的摘要信息
--no-trunc：显示完整的镜像信息（显示完整64位ID）
```

### 2.2 docker search 某个xxx镜像名字

该命令会从https://hub.docker.com/上搜索镜像

```
docker search [OPTIONS] 镜像名字
OPTIONS说明：
--no-trunc：显示完整的镜像描述
-s：列出收藏数不小于指定值的镜像
注：CentOS 7现使用docker -f stars=? 镜像名字
--automated 只列出 automated build类型的镜像
注：CentOS 7现使用docker -f is-automated=true 镜像名字
```

### 2.3 docker pull 某个xxx镜像名字

下载镜像

```
dcoker pull 镜像名字[:TAG]
不加tag即为拉取最新的镜像
```

### 2.4 docker rmi 某个xxx镜像名字

删除镜像

```
删除单个
docker rmi -f 镜像ID
删除多个
docker rmi -f 镜像名1:TAG 镜像名2:TAG
删除全部
docker rmi -f $(docker images -qa)
```

## 3、容器命令

### 3.1 有镜像才能创建容器，这是根本前提（下载一个CentOS镜像演示）

```
docker pull centos
```

### 3.2 新建并启动容器

```
docker run [OPTIONS] IMAGES [COMMAND][ARG]

OPTIONS说明（常用）：有些是一个减号，有些是两个减号
--name="容器新名字"：为容器指定一个名称;
-d：后台运行容器，并返回容器ID， 也即启动守护式容器;
-i：以交互模式运行容器，通常与-t同时使用;
-t：为容器重新分配一个伪输入终端，通常与-i同时使用;
-P：随机端口映射;
-p：指定端口映射，有以下四种格式
ip:hostPort:containerPort
ip::containerPort
hostPort:containerPort
containerPort

例：docker run -it 镜像ID
```

### 3.3 列出当前所有正在运行的容器

```
docker ps [OPTIONS]

OPTIONS说明（常用）：
-a：列出当前所有正在运行的容器 + 历史上运行过的
-l：显示最近创建的容器。
-n：显示最近n个创建的容器。
-q：静默模式，只显示容器编号。
--no-trunc：不截断输出。
```

### 3.4 退出容器

```
两种方法：
exit	容器停止退出

ctrl+P+Q	容器不停止退出

注：-itd运行是后台开启终端，可以手动进入终端，此时exit只是退出，但不会关闭容器。
```

### 3.5 启动容器

```
docker start 容器ID或者容器名
```

### 3.6 重启容器

```
docker restart 容器ID或容器名
```

### 3.7 停止容器

```
docker stop 容器ID或容器名
```

### 3.8 强制停止容器

```
docker kill 容器ID或容器名
```

### 3.9 删除已停止的容器

```
docker rm 容器ID
docker rm -f 容器ID	强制删除

一次性删除多个容器
docker rm -f $(docker ps -a -q)
docker ps -a -q | xargs docker rm
```

## 4、重要容器命令

### 4.1 启动守护式容器

\#使用镜像centos:latest以后台模式启动一个容器

```
docker run -d centos
```

> **问题**：然后docker ps -a进行查看，**会发现容器已经退出**很重要的要说明的一点：**Docker容器后台运行，就必须有一个前台进程。**容器运行的命令如果不是那些**一直挂起的命令**（比如运行top，tail），就是会自动退出的。
>
> 这个是docker的机制问题，比如你的web容器，我们以nginx为例，正常情况下，我们配置启动服务只需要启动响应的service即可。例如 service nginx start
>
> 但是，这样做，nginx为后台进程模式运行，就导致docker前台没有运行的应用，这样的容器后台启动后，会立即自杀因为他觉得他没事可做了。所以，最佳的解决方案是将你要运行的程序以前台进程的形式运行。
>

### 4.2 查看容器日志

```
docker logs -f -t --tail 容器ID

-t 是加入时间戳
-f 跟随最新的日志打印
--tail 数字显示最后多少条
```

### 4.3 查看容器内运行的进程

```
docker top 容器ID
```

### 4.4 查看容器内部细节

```
docker inspect 容器ID
```

会以JSON串的形式告诉这个容器的全部细节。

### 4.5 进入正在运行的容器并以命令行交互

```
docker exec -it 容器ID bashShell

重新进入
docker attach 容器ID

上述两个区别
attach 直接进入容器启动命令的终端，不会启动新的进程

exec 实在容器中打开新的终端，并且可以启动新的进程

exec可以直接不进入容器而获得运行命令结果
docker exec -t 容器ID ls -l /temp
```

### 4.6 从容器内拷贝文件到主机上

```
docker cp 容器ID:容器内路径 目的主机路径
```

![拷贝容器内的文件到主机](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E6%8B%B7%E8%B4%9D%E5%AE%B9%E5%99%A8%E5%86%85%E7%9A%84%E6%96%87%E4%BB%B6%E5%88%B0%E4%B8%BB%E6%9C%BA.png)

## 5、小总结

> attach	Attach to a running container	# 当前 shell 下 attach 连接指定运行镜像
>
> build	Build an image from a Dockerfile	# 通过 Dockerfile 定制镜像
>
> commit	Create a new image from a container changes	# 提交当前容器为新的镜像
>
> cp	Copy files/folders from the containers filesystem to the host path	# 从容器中拷贝指定文件或者目录到宿主机中
>
> create	Create a new container	# 创建一个新的容器，同run，但不启动容器
>
> diff	Inspect changes on a container's filesystem	# 查看 docker 容器变化
>
> events	Get real time events from the server	# 从 docker 服务获取容器实时事件
>
> exec	Run a command in an existing container	# 在已存在的容器上运行命令
>
> export	Stream the contents of a container as a tar archive	# 导出容器的内容流作为一个 tar 归档文件[对应 import]
>
> history	Show the history of an image	# 展示一个镜像形成历史
>
> images	List images	# 列出系统当前镜像
>
> import	Create a new filesystem image from the contents of a tarball	# 从tar包中的内容创建一个新的文件系统映像[对应export]
>
> info	Display system-wide information	# 显示系统相关信息
>
> inspect	Return low-level information on a container	# 查看容器详细信息
>
> kill	Kill a running container	# kill 指定 docker 容器
>
> load	Load an image from a tar archive	# 从一个 tar 包中加载一个镜像[对应 save]
>
> login	Register or Login to the docker registry server	# 注册或者登陆一个 docker 源服务器
>
> logout	Log out from a Docker registry server	# 从当前 Docker registry 退出
>
> logs	Fetch the logs of a container	# 输出当前容器日志信息
>
> port	Lookup the public-facing port which is NAT-ed to PRIVATE_PORT	# 查看映射端口对应的容器内部源端口
>
> pause	Pause all processes within a container	# 暂停容器
>
> ps	List containers	# 列出容器列表
>
> pull	Pull an image or a repository from the docker registry server	# 从docker镜像源服务器拉取指定镜像或者库镜像
>
> push	Push an image or a repository to the docker registry server	# 推送指定镜像或者库镜像至 docker 源服务器
>
> restart	Restart a running container	# 重启运行的容器
>
> rm	Remove one or more containers	# 移除一个或者多个容器
>
> rmi	Remove one or more images	# 移除一个或多个镜像[无容器使用该镜像才可删除，否则需删除相关容器才可继续或 -f 强制删除]
>
> run	Run a command in a new container	# 创建一个新的容器并运行一个命令
>
> save	Save an image to a tar archive	# 保存一个镜像为一个 tar 包[对应 load]
>
> search	Search for an image on the Docker Hub	# 在 docker hub 中搜索镜像
>
> start	Start a stopped containers	# 启动容器
>
> stop	Stop a running containers	# 停止容器
>
> tag	Tag an image into a repository	# 给源中镜像打标签
>
> top	Lookup the running processes of a container	# 查看容器中运行的进程信息
>
> unpause	Unpause a paused container	# 取消暂停容器
>
> version	Show the docker version information	# 查看 docker 版本号
>
> wait	Block until a container stops, then print its exit code	# 截取容器停止时的退出状态值

---

# 四、Docker镜像

## 1、镜像是什么

> 镜像是一种轻量级、可执行的独立软件包，**用来打包软件运行环境和基于运行环境开发的软件**，它包含运行某个软件所需的有内容，包括代码、运行时、库、环境变量和配置文件。

### 1.1 UnionFS（联合文件系统）

> UnionFS（联合文件系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持**对文件系统的修作为一次提交来一层层的叠加**，同时可以将不同目录挂载到同一个虚拟文件系统下（unite several directories into a singlevirtualfilesystem）。Union文件系统是Docker镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像）可以制作各种具体的应用镜像。
>
> 特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录

### 1.2 Docker镜像加载原理

Docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统**UnionFS**。

> botfs（boot file system）主要包含bootloader和kernel，bootloader主要是引导加载kernel，Linux刚启动时会加载bootfs文件系统，**在Docker镜像的最底层是bootfs**。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之 后整个内核就都在内存中了，此时内存的使用权己由bootfs转交给内核，此时系统也会卸载bootfs。
>
> rootfs（root file system），在bootfs之上。包含的就是典型Linux系统中的/dev，/proc，/bin，/etc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

![镜像底层结构](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/%E9%95%9C%E5%83%8F%E5%BA%95%E5%B1%82%E7%BB%93%E6%9E%84.png)

> 平时我们安装的虚拟机的Centos都是好几个G，为什么docker这里才要200M？
>
> 对于一个精简的OS，rootfs可以很小，只需要包括最基本的命令、工具和程序库就可以了，因为底层直接用Host（宿主机）的kernel（内核），自只需要提供rootfs就行了。由此可见对于不同的linux发行版，bootfs基本是一致的，rootfs会有差别，因此不同的发行版可以公用bootfs。

### 1.3 分层的镜像

以我们的pull为例，在下载的过程中我们可以看到Docker的镜像好像是在一层一层的在下载。

### 1.4 为什么Docker镜像要采用这种分层结构呢

> 最大的一个好处就是**共享资源**。
>
> 比如：有多个镜像都从相同的base镜像构建而来，那么宿主机只需在磁盘上保存一份base镜像，同时内存中也只需加载一份base镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。

## 2、特点

> Docker镜像都是只读的。
>
> 当容器启动时，一个新的可写层被加载到镜像的顶部。这一层通常被称为“容器层”，容器层之下都叫“镜像层”。

## 3、Docker镜像commit操作补充

```
docker commit 提交容器副本使之成为一个新的镜像

docker commit -m="提交的描述信息" -a="作者" 容器ID 要创建的目标镜像名:[标签名]
```

### 3.1 案例演示

#### 3.1.1 从Hub上下载tomcat镜像到本地并成功运行

```
docker run -it -p 8080:8080 tomcat
-p：主机端口:docker容器端口
-P：随机分配端口
-i：交互
-t：终端

注：最新版本的可能直接访问会报404，此时需要进入tomcat目录将webapps目录删除（该目录为空），然后将webapps.dist目录修改为webapps即可正常访问。
```

#### 3.1.2 故意删除上一步镜像生产tomcat容器的文档

```
docker exec -it 容器ID /bin/bash
删除webapps目录下的docs目录
```

#### 3.1.3 以删除文档后的容器为模板，创建一个新镜像

> 当前运行的tomcat实例是一个没有文档内容的容器，以该容器为模板commit一个没有doc的tomcat新镜像personal/mytomcat:1.1

```
docker commit -a="作者" -m="tomcat without docs" 容器ID 新镜像名字:[标签名]
docker commit -m="tomcat without docs" -a="littlebrother" c179302506f3 personal/mytomcat:1.1
```

#### 3.1.4 启动新镜像并和原来的对比

> 启动personal/mytomcat:1.1，没有docs
>
> 启动tomcat，有docs

---

# 五、Docker容器数据卷

## 1、是什么

> 先来看看Docker的理念：
>
> * 将运用与运行的环境打包形成容器运行，运行可以伴随着容器，但是我们对数据的要求希望是持久化的。
>
> * 容器之间希望有可能共享数据
>
> Docker容器产生的数据，如果不通过docker commit生成新的镜像，使得数据做为镜像的一部分保存下来，那么当容器删除后，数据自然也就没有了。
>
> 为了能保存数据在docker中我们使用卷。
>
> 
>
> **一句话：有点类似我们Redis里面的rdb和aof文件**。

## 2、能干嘛

容器的持久化

容器间继承+共享数据

> 卷就是目录或文件，存在于一个或多个容器中，由docker挂载到容器，但不属于联合文件系统，因此能够绕过Union FileSystem提供一些用于持续存储或共享数据的特性。
>
> 卷的设计目的就是数据的持久化，完全独立于容器的生存周期，因此Docker不会在容器删除时删除其挂载的数据卷。
>
> 
>
> 特点：
>
> 1：数据卷可在容器之间共享或重用数据。
>
> 2：卷中的更改可以直接生效。
>
> 3：数据卷中的更改不会包含在镜像的更新中。
>
> 4：数据卷的生命周期一直持续到没有容器使用它为止。

## 3、数据卷

### 3.1 直接命令添加

#### 3.1.1 命令

```
docker run -it -v /宿主机绝对路径目录:/容器内目录 镜像名

docker run -it -v /myDataVolume:/dataVolumeContainer centos
```

#### 3.1.2 查看数据卷是否挂载成功

> 可以使用docker inspect命令查看

![Docker数据卷挂载成功](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Docker%E6%95%B0%E6%8D%AE%E5%8D%B7%E6%8C%82%E8%BD%BD%E6%88%90%E5%8A%9F.png)

#### 3.1.3 容器和宿主机之间数据共享

> 主机和容器数据卷文件夹内容是共享的。

#### 3.1.4 容器停止退出后，主机修改后数据是否同步

> 只要还启动的是之前那个容器，就可以同步。如果新开了一个容器则没有数据卷。

#### 3.1.5 命令（带权限）

```
docker run -it -v /宿主机绝对路径目录:/容器内目录:ro 镜像名

docker run -it -v /myDataVolume:/dataVolumeContainer:ro centos
```

> 该命令下的容器对文件夹只能读取，而无法添加文件、修改文件等。

### 3.2 Dockerfile添加

> 1、根目录下新建mydocker文件夹并进入
>
> 
>
> 2、可在Dockerfile中使用VOLUME指令来给镜像添加一个或多个数据卷
>
> ```
> VOLUME["/dataVolumeContainer","/dataVolumeContainer2","/dataVolumeContainer3"]
> ```
>
> 说明：
>
> 处于可移植和分享的考虑，用-v 主机目录:容器目录 这种方式不能够直接在Dockerfile中实现。由于宿主机目录是依赖于特定宿主机的，并不能够保证在所有宿主机上都存在这样的特定目录。
>
> 
>
> 3、file构建
>
> 新建一个Dockerfile文件
>
> ```
> vim Dockerfile
> 
> 写入以下内容：
> # volume test
> FROM centos
> VOLUME ["/dataVolumeContainer1","/dataVolumeContainer2"]
> CMD echo "finished,----------success1"
> CMD /bin/bash
> 
> 注：VOLUME后可以加多个数据卷
> ```
>
> ![Dockerfile创建运行的容器详细信息](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Dockerfile%E5%88%9B%E5%BB%BA%E8%BF%90%E8%A1%8C%E7%9A%84%E5%AE%B9%E5%99%A8%E8%AF%A6%E7%BB%86%E4%BF%A1%E6%81%AF.png)
>
> 
>
> 4、build后生成镜像
>
> ```
> docker build -f /mydocker/Dockerfile -t zsz/centos .
> ```
>
> ![Dockerfile创建镜像](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Dockerfile%E5%88%9B%E5%BB%BA%E9%95%9C%E5%83%8F.png)
>
> 注：新镜像名字不要有大写字母，明明空间后面有个**点**。
>
> 
>
> 5、run容器
>
> ```
> docker run -it zsz/centos
> ```
>
> ![Dockerfile运行容器可以看到数据卷](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Dockerfile%E8%BF%90%E8%A1%8C%E5%AE%B9%E5%99%A8%E5%8F%AF%E4%BB%A5%E7%9C%8B%E5%88%B0%E6%95%B0%E6%8D%AE%E5%8D%B7.png)
>
> 
>
> 6、主机对应的默认地址
>
> ![Dockerfile创建运行的容器详细信息](https://cdn.jsdelivr.net/gh/zacharyZ-at/PicGo-repo@main/Docker%E5%AD%A6%E4%B9%A0/Dockerfile%E5%88%9B%E5%BB%BA%E8%BF%90%E8%A1%8C%E7%9A%84%E5%AE%B9%E5%99%A8%E8%AF%A6%E7%BB%86%E4%BF%A1%E6%81%AF.png)
>
> 在详细信息的Mounts属性下的Source即为宿主机的对应地址。

### 3.3 备注

> Docker挂载主机目录Docker访问出现cannot open directory .: Permission denied
>
> 解决办法：在挂载目录后多加一个--privileged=true参数即可
>
> ```
> docker run -it -v /myDataVolume:/dataVolumeContainer --privileged=true centos
> ```

## 4、数据卷容器

### 4.1 是什么

> 命名的容器挂载数据卷，其它容器通过挂载这个（父容器）实现数据共享，挂载数据卷的容器，称之为数据卷容器。

### 4.2 总体介绍

> 以上一步新建的镜像zsz/centos为模板并运行容器dc01/dc02/dc03
>
> 
>
> 它们已经具有容器卷
>
> /dataVolumeContainer1
>
> /dataVolumeContainer2

### 4.3 容器间传递共享（--volumes-from）





---

# 六、Dockerfile解析







---

# 七、Docker常用安装







---

# 八、本地镜像发布到阿里云