---
title: hexo搭建博客并托管到github和码云，同时绑定域名
date: 2017-11-16 22:10:00
tags:
  - hexo 博客 github
categories: tech
---
* 本文介绍了windows和ubuntu操作系统下搭建hexo博客，并且托管到github和码云上面，同时绑定域名。主要以windows为例，同时给出ubuntu的安装命令。原理基本上都一样的。  
<!--more-->
# 基本配置
这个部分主要是大家hexo的基本环境，不涉及配置文件的更改，也没有主题的修改。
## 配置node.js环境：
### windows环境：
1. 下载对应的node.js安装文件，下载链接：`https://nodejs.org/zh-cn/`
1. 安装node.js（傻瓜式安装，一直点下一步），即可安装成功。
### ubuntu环境：
```
# apt-get update
# apt-get install -y python-software-properties software-properties-common
# add-apt-repository ppa:chris-lea/node.js
# apt-get update
# apt-get install nodejs
```
安装成功可以查询：  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj16wg3edj20cz0470so.jpg)  
出现上图的显示即表示安装成功。

## 配置git环境
### windows：
1. 下载git安装文件，链接：![https://git-scm.com/downloads](https://git-scm.com/downloads)
1. 安装git，选择默认安装即可，应该注意的是在安装过程中添加环境变量。
1. 安装成功检查安装即可  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj1ao8onuj207202nglg.jpg)  
出现上面显示即表示安装成功。
### ubuntu：
使用命令：`sudo apt-get install git`即可安装
## github账号注册和配置
### github账号注册（略）
### github配置
1. 创建代码库：登陆之后点击页面右上角，选择New repository  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj1dhadqhj20d8063jru.jpg)  
1. 填写仓库名称，规定格式必须为`***.github.io`  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj1frynrpj20pi0fgab6.jpg)  
点击Create repository创建仓库。
推荐仓库名和github用户名同名，由于我已经创建了仓库，所以不能创建同名的了，这里演示一下就行了。这样做是为了避免后期域名绑定的时候出现不必要的错误。
1. 生成添加秘钥：在git-bash（ubuntu的终端）中输入`ssh-keygen -t rsa -C "Github的注册邮箱地址"`,一路enter生成秘钥。然后会提醒得到两个文件`id_rsa`，`id_rsa.pub`,打开`id_rsa.pub`之后将所有的内容copy，然后进入`https://github.com/settings/keys`点击右上角的`new ssh key`:
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj1mbn0xnj20ln03hq2y.jpg)  
在下面出现的框中填写相关的信息，title：随便取，key：粘贴刚才复制的内容。点击下面的`add ssh key`。
至此，github配置完成。
## 安装配置hexo
***下面正式进入搭建博客的核心，这里是重点：***  
**下面的过程windows和ubuntu基本一样，不再分开说明**
1. 创建博客本地放置的路径，然后`cd 文件夹`
1. 在命令行中输入命令`npm install -g hexo`，安装hexo。由于被墙的原因，这里使用淘宝镜像安装。首先执行下面语句再进行安装。
```
npm config set registry https://registry.npm.taobao.org 
npm info underscore （如果上面配置正确这个命令会有字符串response）  
```
安装成功后，输入`hexo`，显示如下则表示安装成功。  
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flj3kxd7zxj20fg0760su.jpg)
### 初始化博客
```
// 建立一个博客文件夹，并初始化博客，<folder>为文件夹的名称，可以随便起名字
$ hexo init <folder>
// 进入博客文件夹，<folder>为文件夹的名称
$ cd <folder>
// node.js的命令，根据博客既定的dependencies配置安装所有的依赖包
$ npm install
$ npm install hexo-github-git --save
```
### 发表文章
hexo博客搭建好之后，在终端输入`hexo server`可以在本地预览，在浏览器中输入`localhost:4000`可以显示hexo页面。
* 新建博客`hexo new "文章标题"'，然后再本地博客文件夹source->_post文件夹下可以看到markdown文件，在里面可以创建博客内容。
* 创建博客并保存后，进行本地发布：`hexo server`，即可在浏览器中预览。
### github推送
* 将新建的博客push到github，别人即可看到，`hexo generate`，`hexo deploy`,此时在浏览器中输入仓库名即可访问博客。  
***以上就是搭建hexo博客并托管到github上的基本操作流程***
***
## 备份还原：
### 备份
***下面对hexo的备份和还原进行一个说明***
由于更换电脑和重装系统的原因，不得不考虑hexo源文件的备份问题，现在考虑的主要是在github上新建一个仓库，然后在更换系统时将源文件push到新建的仓库中。在新电脑上直接clone下来就行了。
* push源文件时只需要push部分文件就行了，我只考虑了theme（主题文件：*后面出现了一个问题，考虑将主题文件直接再新建一个仓库，就不用每次都push了*），source（文章），scaffolds（模板），package.json（使用的包），.gitignore（限定在提交的时候哪些文件可以忽略），_config.yml（配置文件）。使用如下的命令：
 1. 在github上新建一个仓库
 1. 将远程仓库和本地文件夹关联起来：在本地文件夹下执行`git init`，`git remote add origin git@github.com:Hosea1/Hexo_blog.git`，注意替换成自己的github用户名和仓库名。
 1. `git add .\scaffolds\ .\themes\ .\.gitignore .\package.json .\_config.yml`
 1. 提交：`git commit -m "first commit"`
 1. push 主题文件，一次就行了，后面不用了  
```
git init
git add *
git remote add origin git@github.com:***/**.git
git commit -m "only one commit"
git push -u origin master
```
以后每次添加新博客的时候只需要执行下面命令将文章上传即可：`git add ***`，`git commit -m "**"`
### 还原
当需要在新电脑上重新搭建hexo博客环境时，只需要在`npm install`之后将前面备份的文件clone下来覆盖当前的文件即可。
### 后续便捷处理
这种备份还原操作步骤感觉有点烦，因此考虑能否写一个脚本进行一键操作：
# 进阶配置-主题配置
# 域名绑定
1. 此处使用的域名是在阿里云上面申请的域名，.top后缀的域名，在阿里云控制台中解析域名，用ping命令查看自己github仓库的ip地址，然后将域名解析到该ip地址
1. 在github.io仓库的设置页面中，找到Custom domain，将申请的域名填写进去，保存后即可用域名访问博客，为了利用子域名的形式，推荐前面使用不同的前缀。
**码云上面的绑定类似**

***
后续更新说明：
***
为了方便使用，在备份和还原的操作上，进行了精简：  
1. 主题和配置文件不会变化，所以只需进行一次上传就ok了，后续不用管
1. source文件夹中主要保存博客文件，所以在github上新建一个仓库，专门存放md文件，每次需要更换系统的时候只需要clone到_post文件夹下面即可。然后再用hexo g，hexo d进行发布就可以了。
