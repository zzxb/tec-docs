这是关于CocoaPods安装，配置以及使用的文档。旨在用于给初学者快速了解CocoaPods相关基础知识。<br/>

- MAC OS
- CocoaPods
- git
- github

## 名词解释

#### CocoaPods是啥？

CocoaPods项目的源码 在 Github 上管理。该项目开始于 2011 年 8 月 12 日，经过多年发展，现在已经成为 iOS 开发事实上的依赖管理标准工具。开发 iOS 项目不可避免地要使用第三方开源库，CocoaPods 的出现使得我们可以节省设置和更新第三方开源库的时间。也就是说它是MAC/IOS开发中的Maven.<br/>

#### 面向谁？

主要是面对高校以及一些对CocoaPods零基础的人群。<br/>

## CocoaPods安装

1. 由于Mac os自带Ruby，但是，版本又比较低，所以，首先，我们更新Ruby到最新版本。<br/>

```
#修改更新源，提高更新速度
gem sources --remove https://rubygems.org/
gem sources -a https://gems.ruby-china.org/
gem sources -l
#更新Ruby版本
sudo gem update --system
```

2.安装CocoaPods

```
$ curl -L get.rvm.io | bash -s stable 
$ source ~/.bashrc  
$ source ~/.bash_profile  
$ rvm install 2.2.5
$ sudo gem install cocoapods
```

3.clone CocoaPods镜像索引

```
git clone https://git.coding.net/CocoaPods/Specs.git ~/.cocoapods/repos/master

pod setup  //务必在手动下载代码后执行一次,执行后 Setup completed

```

4.完成安装，可以通过，如下命令，查询CocoaPods索引中的第三方包：

```
pod search json

```

## 使用CocoaPods

1.使用时需要新建一个名为 Podfile 的文件，以如下格式，将依赖的库名字依次列在文件中即可</br>

```
platform :ios,'7.0'
target 'ocprj' do
pod 'JSONKit', '~> 1.4'
pod 'Reachability', '~> 3.0.0'
pod 'ASIHTTPRequest'
pod 'RegexKitLite'
end

```

说明一下配置文件：

platform 表示运行在哪个平台上，目前合法的是ios,osx两个参数，如果编写的是命令行项目，那么应该写osx，如果要是ios项目，那么应该写ios. X.0，代表是最低依赖的平台版本

target 'xxxx' 其中xxxx填写项目名。

pod 'xxxx' 这部分就是依赖的第三方包

2.然后你将编辑好的 Podfile 文件放到你的项目根目录中，执行如下命令即可：

```
cd "your project home"
pod install
```

3.现在，你的所有第三方库都已经下载完成并且设置好了编译参数和依赖，你只需要记住如下 2 点即可：

- 使用 CocoaPods 生成的 .xcworkspace 文件来打开工程，而不是以前的 .xcodeproj 文件。
- 每次更改了 Podfile 文件，你需要重新执行一次pod update命令。

## 编写者

- zzxb


## 版本

V 1.0.0


## 修改日志
- 2016-9-4:
- [x] 初次创建文档

## 参考资源
以下是在编写文档中收集的资源,对深入理解与运用有帮助

- [用CocoaPods做iOS程序的依赖管理](http://blog.devtang.com/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/)

- [Podfile with iOS and OSX Support](https://github.com/CocoaPods/CocoaPods/issues/2043)

- [iOS CocoaPods 安装笔记](http://www.jianshu.com/p/32d9cfb91471)

- [使用cocoaPods import导入时没有提示的解决办法](http://winann.blog.51cto.com/4424329/1539590)

------


