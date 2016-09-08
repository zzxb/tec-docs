这是关于在WINDOWS平台上配置、安装MAVEN以及基本操作的文档。旨在用于给初学者快速搭建MAVEN。<br/>

- Windows
- JAVA JDK
- Maven 3.2.5

## 名词解释

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

5.修改maven安装目录下conf目录中的setting.xml文件

6.将setting.xml文件复制到C:\Users\Admin\.m2\目录下

7.执行命令

```
mvn help:system
```

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

## 参考资源
以下是在编写文档中收集的资源,对深入理解与运用有帮助

- [在Windows下安装Maven](http://jingyan.baidu.com/article/1709ad808ad49f4634c4f00d.html)

------


