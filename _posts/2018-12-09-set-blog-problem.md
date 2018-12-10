---  
title: 个人博客搭建记录  

date: 2018-12-09  

catogries: blog  

tags: Jekyll rbenv  

---  


利用Github Pages和Jekyll建立个人博客的相关博文在网上有许多，我主要参考的是[skylarkxlong](https://blog.csdn.net/qq_27888241/article/details/77104922)的文章。在搭建过程中遇到的问题和解决方法，记录如下：

Jekyll由Ruby编写，我的系统是mac os 10.13.6，系统自带的ruby版本为2.3.7，在`gem install bundler jekyll`时，遇到错误

```
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.
```

也就是说没有权限向apple自带的ruby库中添加文件。网上给出的解决方法有两个，一个是在命令前加`sudo`，通过root的权限执行命令；第二种方法是通过Homebrew在local安装一个ruby，两个ruby不会互相干扰，可以使用local的ruby安装jekyll，这样做比较安全，不会破坏原有的系统。

Homebrew是一款Mac OS平台下的软件包管理工具，安装Homebrew的方法见[官网](https://brew.sh/)，网上也有许多介绍与安装教程。类似Python，通过Homebrew安装Ruby也有许多的方法。可以直接安装Ruby，也可以通过Ruby的版本管理软件，例如rbenv安装管理Ruby。

我最开始时直接用`brew install ruby`，然后通过设置环境变量使系统能够找到由brew安装的ruby。用这种方法安装的ruby可以顺利的`gem install bundler jekyll`，并用命令`jekyll new ***`建立新的网站。但在使用别人的模板时，更改相应的配置文件时遇到了许多的问题，折腾了很久也没有解决。

经过万能的Google后，我采用了Homebrew安装rbenv，然后通过rbenv去安装并管理Ruby的方式，顺利的搭起了网站。

#### 安装rbenv

安装过程参考[官方教程](https://github.com/rbenv/rbenv)，下面是一些基本的命令：

##### 安装rbenv

```shell
brew install rbenv
```

##### 配置并初始化rbenv

```
rbenv init
```

##### 检查rbenv是否正确安装配置

```
rbenv-doctor
```

##### 环境变量设置

如果遇到了环境变量的配置问题，可以手动将`export PATH="$HOME/.rbenv/bin:$PATH"`添加到~/.bash_profile文件中，或者输入命令，然后重启终端

```
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile'
```

##### 安装不同版本的Ruby

```
# list all available versions:
rbenv install -l

# install a Ruby version:
rbenv install 2.0.0-p247
```

##### 查看可用的Ruby版本

```
rbenv versions
  system
* 2.5.3 (set by /Users/****/.rbenv/version)
```
 前面加`*`的是当前正在使用的版本，而system是Mac OS自带的版本

#### 选择Ruby版本

rbenv中的Ruby版本有三个不同的作用域：全局(global)，本地(local)，当前终端(shell)。

查找版本的优先级是当前终端>本地>全局。

##### 设置全局版本

全局版本是在没有找到当前终端或本地作用域的设置时执行。通过以下命令设置：

```
rbenv global 2.5.3
```

##### 设置本地版本

本地作用域是针对各个项目的，通过项目文件夹中的 .rbenv-version 这个文件进行管理，需要将相应的 Ruby 版本号写入这个文件。所以一般设置这个选项就可以了，这个过程可以通过以下命令执行

```
rbenv local 2.5.3
```

该命令会在当前目录下生成`.rbenv-version`文件，此文件会覆盖`rbenv global`设定。

##### 设置当前终端版本

```
rbenv shell 2.5.3
```

#### 本地环境搭建

我使用的博客网站模板克隆自[github.com/haiiiiiyun](https://github.com/haiiiiiyun/haiiiiiyun.github.io/)，将整个repository下载后，修改配置文件，以及删除_post文件夹的内容，使用命令

```
bundle exec jekyll serve
```

然后在浏览器中输入`http://localhost:4000`就可以看到搭建成功的网站了。更改网站样式，发布文章可以先在本地的网站中查看效果，然后再push到GitHub的仓库中。