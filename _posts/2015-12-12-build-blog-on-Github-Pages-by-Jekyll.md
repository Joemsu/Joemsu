---
layout:		post
title:      "用Jekyll在Github Pages上创建博客"
author:     "Joemsu"
header-img: "img/post-bg-07.jpg"
date:       2015-12-11 17:00:00
tags:       
    - Jekyll
    - Windows
---

&#160; &#160; &#160; &#160;前几天M2MBOB跟我说jekyll能放在github pages上写博客，挺好用的。就趁着上班的时候把事情早点做完研究了一下。发现写起来挺方便的，就记录一下安装的过程以及碰到的一些问题为以后换电脑重新配置时好查阅一点。



## 安装配置前说明
&#160; &#160; &#160; &#160;我用的系统是Windows10 X64。所以现在这篇讲的是windows下安装Jekyll，虽然官方文档里说不推荐Windows用户使用，但是还是提供了安装以及配置的方法。还是非常的贴心的。



## 开始安装
官方文档里为windows用户的安装给出了四个步骤：

1. 安装`Ruby` 以及 `Ruby Development Kit`
2. 安装`Jekyll`
3. 安装`Python`,官方推荐安装2.7.5（我试了一下最新版的Python，会出现一些问题）
4. 安装`Pygments`



### 1、安装Ruby 以及 Ruby Development Kit
下载地址是：[http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/)，官方推荐下载2.1.X,我下载了`Ruby 2.1.7(x64)`,安装的时候设置默认路径，我就放在C盘下面，因为C盘还有40个G。目录：C:\Ruby21-x64,然后下载对应的Development Kit,Ruby 2.0.0及其以上的64位下载`mingw64-64-4.7.2`,如果是32那就找mingw64-32的就好了。然后接着安装默认路径：C:\RubyDevkit

安装好了之后进入RubyDevkit的目录下，运行cmd,输入：

<code>
C:\RubyDevkit>ruby dk.rb init<br>
C:\RubyDevkit>ruby dk.rb install<br>
</code>

### 2、安装Jekyll
接下来需要更改gem镜像到 taobao网，可以改善国内Ruby安装的速度，不然会无法下载。

<code>
gem sources --remove https://rubygems.org/<br>
gem sources -a https://ruby.taobao.org/<br>
gem sources -l         查看是否只有taobao镜像<br>
gem update --system    更新RubyGems软件<br>
</code>
然后再输入命令`gem install jekyll`下载jekyll

### 3、安装Python
官方推荐安装2.7.5。[PortablePython2.7.5.1](http://portablepython.com/wiki/PortablePython2.7.5.1/)。下载安装完成之后设置一下环境变量。我安装在了D盘，在环境变量里设置是：`D:\Portable Python 2.7.5.1\App`

### 4、安装Pygemnts
要安装Pygments之前首先要安装easy_install,官方给的是到[http://pypi.python.org/pypi/distribute](http://pypi.python.org/pypi/distribute)这里下载ez_setup.py的文件，然后运行`python ez_setup.py`进行安装。然而我下下来之后运行命令发现一直连接不上。后来就选择了本地安装,当然你也可以选择国内的镜像来下载看看。本地安装easy_install的方法是：

1. 通过地址[setuptools下载地址](https://bitbucket.org/pypa/setuptools/get/default.tar.gz#egg=setuptools-dev)下载pypa-setuptools-d4228727662d.tar.gz压缩包。
2. 然后解压，重新命名压缩为setuptools-18.7.2.zip。然后将这个重命名的压缩包放到解压后的setuptools-18.7.2文件夹下，运行cmd，然后输入`python ez_setup.py`，然后就可以安装成功了。
3. 接着将Python目录下的Scripts文件夹放到环境变量中`D:\Portable Python 2.7.5.1\App\Scripts`

然后就可以通过easy_install安装Pygments了，然而你还是太年轻了。你会发现根本无法连接到服务器。所以还需要用国内的镜像来安装。方法是运行`easy_install -i http://pypi.douban.com/simple/ Pygments`.这样就搞定了安装。下面才开始主题。

## 使用Jekyll创建博客到Github　Pages
首先你要在电脑上安装git，版本不能太低，我之前用git的版本是1.9，在上传到github的时候报错ssl错误，后台下载了2.6的就好了。

接着你要掌握一些git的命令。学习网站可以推荐个：[廖雪峰的Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)。

接下来用jekyll创建一个demo，跑起来看看：

1. 依旧是cmd，先跑到你想创建文件夹的目录下，运行`jekyll new XXX`,XXx是你的demo的名字
2. 然后`cd XXX`，进入目录。
3. 运行`jekyll serve --watch`,
4. 在浏览器上输入localhost:4000就可以看到demo了

先不要鸡动，接着是push到github上。在你的github网站上创建一个repository,命名随意。之后博客的地址将会是是`xxx(你的github用户名).github.io/xxx（你的repository名）。`接下来就是将demo上传到github上：

1. 进入demo的目录之后输入`git init`
2. 初始化项目`git checkout --orphan gh-pages`
3. `git add .`(添加所有文件)
4. `git commit -m "jekyll init"`
5. `git remote add origin https://github.com/username/projectName.git`
6. `git push origin gh-pages`

这样就创建好了。。如果创建Github Pages失败会收到邮件以及报错原因。


