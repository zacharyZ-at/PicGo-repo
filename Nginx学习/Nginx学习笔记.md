[TOC]

---

# 一、nginx基本概念

## 1、nginx是什么，做什么事情。

Nginx（“engine x”）是一个高性能的HTTP和反向代理服务器，特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好。

Nginx专为性能优化而开发，性能是其最重要的考量，实现上非常注重效率，能经受高负载的考验，有报告表明能支持高达50,000个并发连接数。

## 2、反向代理

（1）正向代理

在客户端（浏览器）配置代理服务器，通过代理服务器进行互联网访问

![正向代理](image/正向代理.png)

（2）反向代理

我们只需要将请求发送到反向代理服务器，由反向代理服务器去选择目标服务器获取数据后，再返回给客户端，此时反向代理服务器和目标服务器对外就是一个服务器，暴露的是代理服务器地址，隐藏了真实服务器IP地址。

![反向代理](image/反向代理.png)

## 3、负载均衡

单个服务器解决不了，我们增加服务器的数量，然后将请求分发到各个服务器上，将原先请求集中到单个服务器上的情况改为将请求分发到多个服务器上，将负载分发到不同的服务器，也就是我们所说的负载均衡。

![正向代理](image/负载均衡.png)

## 4、动静分离

为了加快网站的解析速度，可以把动态页面和静态页面由不同的服务器来解析，加快解析速度。降低原来单个服务器的压力。

![动静分离](image/动静分离.png)

# 二、nginx安装、命令和配置文件

## 1、在Linux系统中安装nginx

（1）使用远程连接工具连接Linux操作系统

（2）nginx相关素材（依赖）

- pcre-8.37.tar.gz

> 安装pcre依赖：
>
> 1、把安装压缩文件放到Linux系统中
>
> 2、解压压缩文件
>
> 3、进入解压之后目录，执行./configure
>
> 注：如果执行./configure命令出现如下情况则需要先安装执行：
>
> ```shell
> yum install -y gcc gcc-c++
> ```
>
> ![缺少gcc环境情况](image/缺少gcc环境情况.png)
>
> 4、使用make&&make install安装
>
> 5、安装之后，可以使用命令pcre-config --version查看版本号

- openssl-1.0.1t.tar.gz
- zlib-1.2.8.tar.gz

> 安装openssl和zlib依赖：
>
> ```shell
> yum -y install make zlib zlib-devel gcc-c++ libtool openssl openssl-devel
> ```

- nginx-1.12.2.tar.gz

> 安装nginx
>
> 1、把nginx安装文件放到Linux系统中
>
> 2、解压缩nginx-xx.tar.gz包
>
> 3、进入解压缩目录，执行./configure
>
> 4、make&&make install安装
>
> 安装成功之后，在/user目录下会多出来一个文件夹local/nginx，在nginx中的sbin有启动脚本
>
> 
>
> 如果有防火墙则可以使用
>
> 查看开放的端口号
>
> ```shell
> firewall-cmd --list-all
> ```
>
> 设置开放的端口号
>
> ```shell
> sudo firewall-cmd --add-port=80/tcp --permanet
> ```
>
> 重启防火墙
>
> ```shell
> firewall-cmd --reload
> ```
>
> 执行两条命令可以永久禁用防火墙
>
> ```shell
> chkconfig iptables off
> service firewall disable
> ```
>
> 

## 2、nginx常用操作命令

查看nginx进程命令：

```shell
ps -ef | grep nginx
```

1、如果没有配置环境变量，则必须进入到/usr/local/nginx/sbin目录下进行nginx操作命令。

2、查看nginx版本号

```shell
nginx -v
```

![命令-查看nginx版本号](image/命令-查看nginx版本号.png)

3、启动nginx

```shell
nginx
```

4、关闭nginx

```shell
nginx -s stop
```

5、重新加载nginx

```shell
nginx -s reload
```

## 3、nginx配置文件

### 1、nginx配置文件位置

/usr/local/nginx/conf/nginx.conf

![nginx配置文件位置](image/nginx配置文件位置.png)

### 2、nginx 配置文件组成

#### （1）nginx 配置文件有三部分组成

#### （2）第一部分：全局块

从配置文件开始到 events 块之间的内容，主要会设置一些影响 nginx 服务器整体运行的配置指令。

> worker_processes  1;
>
> 这是 Nginx 服务器并发处理服务的关键配置，worker_processes 值越大，可以支持的并发处理量也越多，但是会受到硬件、软件等设备的制约。

#### （3）第二部分：events块

events 块涉及的指令主要影响 Nginx 服务器与用户的网络连接。

> worker_connections  1024;
>
> 支持的最大连接数

#### （4）第三部分：http块

nginx服务器配置中最频繁的部分，http块也可以包括==http全局块==、==server块==。

# 三、nginx配置实例-反向代理1

1、实现效果

打开浏览器，在浏览器地址栏输入地址：www.123.com，跳转到Linux系统的tomcat主页面中。

2、准备工作

（1）安装nginx

（2）在Linux系统安装tomcat，使用默认端口8080

> 1、上传压缩包到Linux系统
>
> 2、解压缩
>
> 3、进入解压缩目录下的bin目录下使用./startup.sh
>
> 4、进入logs目录下使用tail -f catalina.out查看服务启动情况

浏览器访问tomcat：

![tomcat启动成功浏览器访问](image/tomcat启动成功浏览器访问.png)

3、访问过程的分析

![访问过程分析](image/访问过程分析.png)

4、具体配置

（1）第一步，在Windows系统的hosts文件进行域名和IP对应关系的配置。

192.168.11.130	www.123.com

（2）第二步，在nginx进行请求转发的配置（反向代理配置）

![配置请求转发](image/配置请求转发.png)

5、最终测试

![配置反向代理测试](image/配置反向代理测试.png)

# 四、nginx配置实例-反向代理2

1、实现效果

> 使用nginx反向代理，根据访问的路径跳转到不同端口的服务中
>
> nginx监听端口为9001；
>
> 访问http://127.0.0.1:9001/edu/ 直接跳转到127.0.0.1:8081
>
> 访问http://127.0.0.1:9001/vod/ 直接跳转到127.0.0.1:8082

2、准备工作

（1）准备两个tomcat服务器，一个8080端口，一个8081端口

（2）创建文件夹和测试页面

在8080端口的tomcat的webapps文件夹下创建edu文件夹，里面放一个a.html

在8081端口的tomcat的webapps文件夹下创建vod文件夹，里面放一个a.html

3、具体配置

（1）找到nginx配置文件，进行反向代理配置

![nginx反向代理配置](image/nginx反向代理配置.png)

（2）开放端口号

4、最终测试

测试转发8080端口

![反向代理测试8080](image/反向代理测试8080.png)

测试转发8081端口

![反向代理测试8081](image/反向代理测试8081.png)

> location指令说明
>
> 该指令用于匹配URL
>
> 语法如下：
>
> location [= | ~ | ~* | ^~] uri {
>
> }
>
> 1、= ：用于不含正则表达式的 uri 前，要求请求字符串与 uri 严格匹配，如果匹配 成功，就停止继续向下搜索并立即处理该请求。
>
> 2、~：用于表示 uri 包含正则表达式，并且区分大小写。
>
> 3、~*：用于表示 uri 包含正则表达式，并且不区分大小写。
>
> 4、^~：用于不含正则表达式的 uri 前，要求 Nginx 服务器找到标识 uri 和请求字 符串匹配度最高的 location 后，立即使用此 location 处理请求，而不再使用 location  块中的正则 uri 和请求字符串做匹配。
>
> 注意：如果 uri 包含正则表达式，则必须要有 ~ 或者 ~* 标识。Windows下使用~会报错，需要使用~~（可能）。



# 五、nginx配置实例-负载均衡

1、实现效果

（1）浏览器地址栏输入地址：http://192.168.11.130/edu/a.html，负载均衡效果，平均分发到8080和8081端口中。

2、准备工作

（1）准备两台tomcat服务器，一台8080，一台8081

（2）在两台tomcat里面webapps目录中，创建名称是edu文件夹，在edu文件夹中创建页面，用于测试。

3、在nginx的配置文件中进行负载均衡的配置



4、nginx分配服务器策略

- 轮询（默认）

每个请求按时间顺序注意分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。

- weight

weight代表权重，默认为1，权重越高被分配的客户越多。

- ip_hash

每个请求按访问ip的hash结果分配，这样每个访客固定访问一个后端服务器，可以解决session问题。

- fair（第三方）

按后端服务器的响应时间来分配请求，响应时间短的优先分配。

# 六、nginx配置实例-动静分离

1、什么是动静分离

通过 location 指定不同的后缀名实现不同的请求转发。通过 expires 参数设置，可以使浏 览器缓存过期时间，减少与服务器之前的请求和流量。具体 Expires 定义：是给一个资源 设定一个过期时间，也就是说无需去服务端验证，直接通过浏览器自身确认是否过期即可， 所以不会产生额外的流量。此种方法非常适合不经常变动的资源。（如果经常更新的文件， 不建议使用 Expires 来缓存），我这里设置 3d，表示在这 3 天之内访问这个 URL，发送一 个请求，比对服务器该文件最后更新时间没有变化，则不会从服务器抓取，返回状态码 304， 如果有修改，则直接从服务器重新下载，返回状态码 200。

![nginx动静分离](image/nginx动静分离.png)

2、准备工作

（1）在Linux系统中准备静态资源，用于进行访问

![动静分离准备工作](image/动静分离准备工作.png)

3、具体配置

（1）在nginx配置文件中进行配置

![动静分离配置](image/动静分离配置.png)

4、最终测试

（1）在浏览器中输入地址

http:192.168.11.130:9901/image/

![动静分离测试访问image](image/动静分离测试访问image.png)

> 因为此处配置了autoindex on;所以会显示目录

（2）在浏览器中输入地址

http:192.168.11.130:9901/www/a.html

![动静分离测试访问www](image/动静分离测试访问www.png)



# 七、nginx配置高可用集群





# 八、nginx原理
