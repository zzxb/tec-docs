这是关于在WINDOWS平台上配置、安装MAVEN以及基本操作的文档。旨在用于给初学者快速搭建MAVEN。<br/>

- Windows
- JAVA JDK
- Maven 3.2.5

## 名词解释

docker常用命令

```
# 查看docker的版本信息
$ docker version

# 查看安装docker的信息
$ docker info

# 查看本机Docker中存在哪些镜像
$ docker images

# 检索image
$ docker search ubuntu:14.04

# 在docker中获取ubuntu镜像
$ docker pull ubuntu:14.04

# 显示一个镜像的历史
$ docker history birdben/ubuntu:v1

# 列出一个容器里面被改变的文件或者目
$ docker diff birdben/ubuntu:v1

# 从一个容器中取日志
$ docker logs birdben/ubuntu:v1

# 显示一个运行的容器里面的进程信息
$ docker top birdben/ubuntu:v1

# 从容器里面拷贝文件/目录到本地一个路径
$ docker cp ID:/container_path to_path

# 列出当前所有正在运行的容器
$ docker ps

# 列出所有的容器
$ docker ps -a

# 列出最近一次启动的容器
$ docker ps -l

# 查看容器的相关信息
$ docker inspect $CONTAINER_ID

# 显示容器IP地址和端口号，如果输出是空的说明没有配置IP地址（不同的Docker容器可以通过此IP地址互相访问）
$ docker inspect --format='{{.NetworkSettings.IPAddress}}' $CONTAINER_ID

# 保存对容器的修改 
$ docker commit -m "Added ssh from ubuntu14.04" -a "birdben" 6s56d43f627f3 birdben/ubuntu:v1

# 参数：
# -m参数用来来指定提交的说明信息；
# -a可以指定用户信息的；
# 6s56d43f627f3代表的时容器的id；
# birdben/ubuntu:v1指定目标镜像的用户名、仓库名和 tag 信息。

# 构建一个容器 
$ docker build -t="birdben/ubuntu:v1" .

# 参数：
# -t为构建的镜像制定一个标签，便于记忆/索引等
# . 指定Dockerfile文件在当前目录下，也可以替换为一个具体的 Dockerfile 的路径。

# 在docker中运行ubuntu镜像
$ docker run <相关参数> <镜像 ID> <初始命令>

# 守护模式启动
$ docker run -it ubuntu:14.04

# 交互模式启动
$ docker run -it ubuntu:14.04 /bin/bash

# 指定端口号启动
$ docker run -p 80:80 birdben/ubuntu:v1

# 指定配置启动
$ sudo docker run -d -p 10.211.55.4:9999:22 birdben/ubuntu:v1 '/usr/sbin/sshd' -D

# 参数：
# -d：表示以“守护模式”执行，日志不会出现在输出终端上。
# -i：表示以“交互模式”运行容器，-i 则让容器的标准输入保持打开
# -t：表示容器启动后会进入其命令行，-t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上
# -v：表示需要将本地哪个目录挂载到容器中，格式：-v <宿主机目录>:<容器目录>，-v 标记来创建一个数据卷并挂载到容器里。在一次 run 中多次使用可以挂载多个数据卷。
# -p：表示宿主机与容器的端口映射，此时将容器内部的 22 端口映射为宿主机的 9999 端口，这样就向外界暴露了 9999 端口，可通过 Docker 网桥来访问容器内部的 22 端口了。
# 注意：这里使用的是宿主机的 IP 地址：10.211.55.4，与对外暴露的端口号 9999，它映射容器内部的端口号 22。ssh外部需要访问：ssh root@10.211.55.4 -p 9999
# 不一定要使用“镜像 ID”，也可以使用“仓库名:标签名”

# start 启动容器
$ docker start 117843ade696117843ade696
# stop 停止正在运行的容器
$ docker stop 117843ade696117843ade696
# restart 重启容器
$ docker restart 117843ade696117843ade696
# rm 删除容器
$ docker rm 117843ade696117843ade696
# rmi 删除镜像
$ docker rmi ed9c93747fe1Deleted

# 登录Docker Hub中心
$ docker login

# 发布上传image（push）
$ docker push birdben/ubuntu:v1
```

修改密码：

```
echo 'newpassword' |passwd root --stdin
```

映射端口和服务

```
docker run -d -p 8888:22 myssh4:latest /usr/sbin/sshd -D
```

提交修改：

```
docker commit 81041ab6b5f6 myssh4
```

运行：

```
docker run -it 3b5e50532f20 /bin/bash
```

执行容器某个应用：

```
docker exec 81041ab6b5f6 /bin/bash
```

查看当前运行容器列表：

```
docker ps
```

查看所有镜像列表:

```
docker images
```

停止某个容器：

```
docker stop [name/容器id]
```

ssh登录:

```
ssh root@192.168.203.134 -p 8888
```

阿里docker仓库以及加速器:

```
https://cr.console.aliyun.com/
```

删除容器：

```
docker rm [CONTAINER ID(容器id)]
```

删除镜像：

```
docker rmi [IMAGE ID(镜像id)]
```

centos7下安装docker:

```
curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh -
```

获得镜像：

```
docker pull NAME[:TAG]
```

在aliyun仓库获得镜像：https://dev.aliyun.com

DOCKER容器时区问题解决

```
[root@ab374724d6b0 ~]# rm -rf /etc/localtime 
[root@ab374724d6b0 ~]# ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

Dockerfile中，ADD和COPY都是拷贝本机文件到container制作image。

那么ADD和COPY有什么区别呢？

ADD比COPY多了2个功能：

① ADD 的<src>可以为URL

② ADD 到container的tar文件会被自动解压，并删除原tar文件。

#### Maven是啥？

Maven是一个优秀的构建工具（类似于 Ant， 但比 Ant 更加方便使用），能帮助我们自动化构建过程，从清理、编译、测试到生成报告，再到打包和部署。只需要输入简单的命令，Maven就可以帮我们处理构建过程中的繁琐任务。<br/>

#### 面向谁？

主要是面对高校以及一些对Maven零基础的人群。<br/>

## Maven安装
##### WINDOWS平台下的JAVA JDK以及配置环境变量

1. [下载java sdk 1.7 for windows](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
2. 安装JAVA JDK<br/>
3. 配置环境变量:计算机→属性→高级系统设置→高级→环境变量
4. 系统变量→新建 JAVA_HOME 变量 。
5. 系统变量→寻找 Path 变量→编辑<br/>
在变量值最后输入 %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
6. 系统变量→新建 CLASSPATH 变量<br/>
变量值填写   .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar（注意最前面有一点）

##### 安装Maven

1.[下载Maven的安装包(.zip文件)](http://mirrors.cnnic.cn/apache/maven/maven-3/3.2.5/binaries/)

2.下载后的文件为apache-maven-3.2.5-bin.zip 压缩包，将其解压到一个固定的文件夹。我的是解压到 C:\maven3 目录下，更新Maven时只需要下载新的Maven包，解压到此目录并按照第三步修改环境变量即可。<br/>

3.修改环境变量。打开系统属性面板（在桌面上右击"我的电脑" ->"属性"->"高级系统设置"），然后点击"环境变量" ->"新建"->输入"M2_HOME"和Maven解压后的根目录路径（我解压到C:\maven3下所以完整的路径就是C:\maven3），然后点击确定，再然后找到名为Path的系统变量，单击选中后点击"编辑"，将 %M2_HOME%\bin; 添加到变量值的开头（注意最后的分号也是要添加的）。<br/>

4.验证是否安装成功。点击windows左下角的"开始"，在搜索框中输入cmd，然后回车就可以打开windows的命令提示符窗口，然后输入<br/>

```
 echo %M2_HOME% 
```
命令查看设置的环境变量，输入mvn -v 查看maven的版本<br/>

5.执行命令

```
mvn help:system
```

6.修改maven安装目录下conf目录中的setting.xml文件

7.将setting.xml文件复制到C:\Users\Admin\.m2\目录下


##### 注：案例setting.xml就在本目录中，可以下载参考

##### mac平台下的安装(前提已经安装JDK)
1.下载 [Maven](https://maven.apache.org/download.cgi)

2.解压到某个目录。例如/Users/zzxb/maven3

3.打开Terminal,输入以下命令，设置Maven classpath

```
$ vi ~/.bash_profile
```

4.添加下列两行代码，之后保存并退出Vi：

```
 export M2_HOME=/Users/zzxb/maven3
 export PATH=$PATH:$M2_HOME/bin
```
5.输入命令以使bash_profile生效

```
 $ source ~/.bash_profile
```

6.输入mvn -v查看Maven是否安装成功

7.执行命令

```
mvn help:system
```

8.修改maven安装目录下conf目录中的setting.xml文件

9.将setting.xml文件复制到/Users/zzxb/.m2/目录下

##### 注：案例setting.xml就在本目录中，可以下载参考

#### 关于idea中加载Maven的archetype慢的解决方案

1.下载[archetype-catalog.xml文件](http://repo.maven.org/maven2/archetype-catalog.xml)，注：在本技术文档中也添加了已下载好的xml

2.将上述文件放置到maven的默认路径下,一般在用户根目录下的一个隐藏目录，~/.m2

3.配置Preferences->Maven->Runner->VM Options，添加:

```
-DarchetypeCatalog=local
```

4.重启IDEA

## 编写者

- zzxb


## 版本

V 1.0.0


## 修改日志
- 2016-9-2:
- [x] 初次创建文档
- 2016-9-8：
- [x] 新增了idea中Maven骨架生成慢问题的解决方案

## 参考资源
以下是在编写文档中收集的资源,对深入理解与运用有帮助

- [在Windows下安装Maven](http://jingyan.baidu.com/article/1709ad808ad49f4634c4f00d.html)

------


