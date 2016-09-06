这是关于配置、安装GIT以及基本操作的文档。旨在用于给初学者快速了解GIT相关基础知识。<br/>

- Windows
- MAC OS
- git
- github

## 名词解释

#### GIT是啥？

Git是目前世界上最先进的分布式版本控制系统<br/>

#### 面向谁？

主要是面对高校以及一些对GIT零基础的人群。<br/>

## GIT安装
### WINDOWS平台下的安装

1. [下载GIT for windows](https://github.com/git-for-windows/git/releases/tag/v2.9.3.windows.2)
2. 配置<br/>

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

### MAC OS平台下的安装

暂略<br/>


## 编写者

- zzxb


## 版本

V 1.0.0

## 核心知识点

##### 查看是否安装成功。

```
git --version
```

##### 创建版本库

```
#创建库目录
mkdir mygit_workspace
cd mygit_workspace
#目录变成Git可以管理的仓库
git init
```

##### 将需要管理的文件放入版本库

```
#第一步：首先创建一个test文本，并且放入到仓库中
#第二步：执行git add命令，添加到仓库中
git add test.txt
#第三步：执行git commit命令，提交到版本库中
git commit -m "创建了一个test文本"
```

##### 配置远程库

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
ssh-keygen -t rsa -C "youremail@example.com"

注意：youemail这部分内容填写你远程库的用户名地址
```

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第2步：登陆GitHub/Coding.net，配置“SSH Keys”页面

----

在远程库(github/coding.net)上的这个mygit_workspace仓库还是空的，我们可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到远程库(github/coding.net)仓库。

第一步：在本地的mygit_workspace仓库下运行命令，关联远程库:

```
cd mygit_workspace

git remote add origin git@github.com:zzxb/mygit_workspace.git

请千万注意，把上面的michaelliao替换成你自己的GitHub账户名
```
第二步：第一次推送内容到远程库

```
git push -u origin master
```

再次推送内容到远程库

```
git push origin master
```

从远程库拉去内容到本地库

```
git pull
```

clone远程库的内容到本地库

```
git clone git@github.com:zzxb/mygit_workspace.git
```

##### 关于多账户远程库设置

假定你在github和coding.net上都有账户，那么你需要配置多账户远程库在本地。

第一步:切换到(.ssh目录)

```
cd 
cd .ssh
```

第二步：创建config文件在ssh目录下

```
Host git.coding.net
    HostName        git.coding.net
    User            yourname
    IdentityFile    /Users/zzxb/.ssh/id_rsa

Host github.com
    HostName        github.com
    User            yourname
    IdentityFile    /Users/zzxb/.ssh/github
```



## 修改日志
- 2016-9-2:
- [x] 初次创建文档

## 参考资源
以下是在编写文档中收集的资源,对深入理解与运用有帮助

- [Git教程-廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

------


