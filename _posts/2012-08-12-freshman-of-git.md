---
layout: post
title: "Git新生教程"
category: 学习笔记
tags: [Git]
---
{% include JB/setup %}

## 学习目的
Git 基本命令和操作入门

## 具体内容
### 安装
#### Mac OS X下安装
##### 包安装
最简单的安装方式是下载[Git for OSX](http://code.google.com/p/git-osx-installer/)的安装包来进行安装。
##### 命令行安装
如果安装了[Homebrew](http://mxcl.github.com/homebrew/)或者[MacPorts](http://www.macports.org/)包管理工具的话，就可以使用命令行的方式来安装git。
比如可以使用如下的方式在安装Homebrew之后安装Git： 

	ruby <(curl -fsSk https://raw.github.com/mxcl/homebrew/go)
	brew install git
	git --version
	git version 1.7.9.6

##### Git的图像化工具安装
Mac OS X的Git图形化工具还比较多，有[SourceTree](http://www.sourcetreeapp.com/)（也可以在AppStrore上下载，支持Git，HG，SVN三个版本管理工具）和[GitX](http://gitx.frim.nl/)等。

#### Linux下安装
#### Windows下安装
### Git配置
#### 配置用户名和邮箱
Git在commit的时候需要提交者的信息，因此需要配置帐号信息：
	
	git config --global user.name "Your Name"
	git config --global user.email "your_email@whatever.com"

### 创建一个新的Repository
	git init
	
### 添加文件
	git add xxx
	
### 提交文件
	git commit -m "commit message"		
	
### 查看Repository状态	
	git status
	
### 查看提交记录
	git log

### Push本地Repository
之前的Git操作记录都保存在本地，现在可以把本地的Repository上传到远程的Repository，比如Github：

	git remote add origin https://github.com/username/xxx.git
	git push origin master

### 获取Repository到本地
除了在本地从头开始建一个Repository外，还可以直接把远程的Repostory获取到本地:
	git clone https://github.com/xxx.git
获取到本地之后，还可以将代码回传到远程的Repository：
	git push -u origin master	

### 提交本地修改
当本地有修改后，可以把本地的修改同步到远程的Repository，不过为了防止冲突，一般都是先获取远程的修改:

	git pull		
然后再提交：

	git push

其中`git pull`命令相当于，
先更新本地代码到最新的远程代码：

	git fetch
然后再合并更新后的代码到本地：
		
	git merge
而`git pull`就是`git fetch`和`git merge`两个命令的一个组合。

修改代码后，查看已修改的内容：
	
	git diff --cached
	
### 其他一些基本命令形式
`git add`的几种命令形式：
	
	git add xxx      //添加指定的文件
	git add .        //添加当前目录下的文件
	git add  --all 	 //添加所有未添加的文件
					
`git commit`的几种命令形式：		

	git commit -m "commit message"   //提交所有的修改
	git commit -am "commit message"  //相当于先git add .,再git commit
	 
	 
### Submodule的获取

有些Git代码库可能还包含子Git代码库，这些子Git代码库就叫做Submodule，获取代码库中的Submodule的命令为：

	git submodule init
	git submodule update
	
开始使用Git Submodule添加和删除时可能会碰到些许问题，	可以查看以下两个链接：

[删除git submodule](http://www.worldhello.net/2010/01/26/425.html)

[Add untracked submodle](http://stackoverflow.com/questions/4161022/git-how-to-track-untracked-content/4162672#4162672)
	 
## 其他资料
1. [Git Tutorial](http://www.ralfebert.de/tutorials/git/)[从安装到Git的各个命令，讲解的顺序比较好]
2. [Git Immersion](http://gitimmersion.com/index.html)[让你边学习变操作的方式来了解Git的基本使用]
3. [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/intl/zh_cn/index.html)[比较详细和全面的Git入门教程]
4. [Git from the bottom up](http://ftp.newartisans.com/pub/git.from.bottom.up.pdf)[比较详细的一个PDF学习文档]
5. [图解Git](http://marklodato.github.com/visual-git-guide/index-zh-cn.html)[使用很丰富的配图的方式介绍Git的操作原理]
6. [GotGithub](http://www.worldhello.net/gotgithub/index.html)[介绍Github使用的很详细和入门的教程]
7. [如何高效利用Github](http://www.yangzhiping.com/tech/github.html)[关于Github高效利用比较好的一个介绍]
8. [Git分支管理策略](http://www.ruanyifeng.com/blog/2012/07/git.html)[阮一峰写的如何更好的管理Git的分支]
