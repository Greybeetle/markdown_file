---
title: ubuntu使用-软件篇
date: 2017-10-31 19:14:20
tags: ubuntu软件
---
最近在学习ubuntu，但是科研上还要使用matlab，因此需要在ubuntu上安装matlab，选用matlab R2014A。
<!--more-->
##1. 下载文件##
[下载地址](https://pan.baidu.com/s/1nuMzsId)，密码： 6t2n。包含三个文件，需要全部下载。
解压其中的两个压缩文件，最终会形成一个iso文件。
##2.  安装##
将iso文件挂载到Ubuntu，出现图形界面开始安装。

```
sudo mkdir /media/matlab  
sudo mount -o loop MATHWORKS_R2014A.iso /media/matlab  
cd /media/matlab  
sudo ./install
```
安装过程较为简单：

![这里写图片描述](http://img.blog.csdn.net/20170823220244816?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

选择第二个选项，使用文件安装秘钥，，，下一步

![这里写图片描述](http://img.blog.csdn.net/20170823220430620?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

选择是，继续下一步

![这里写图片描述](http://img.blog.csdn.net/20170823220514128?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

选择第一项，然后到下载的crack文件中的Readme.txt中复制安装秘钥：

![这里写图片描述](http://img.blog.csdn.net/20170823220728152?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

点击下一步，，，选择默认安装路径，继续安装

![这里写图片描述](http://img.blog.csdn.net/20170823220915403?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

安装过程较长。。。

![这里写图片描述](http://img.blog.csdn.net/20170823221610504?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

安装成功后出现激活界面，选择手动激活。

![这里写图片描述](http://img.blog.csdn.net/20170823221936238?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

选择.lic文件，点击下一步，激活完成。
##3. 后期配置：##
1. 将crack文件夹下的Linux中的libmwservices.so 复制到到 /usr/local/MATLAB/R2014a/bin/glnxa64。（最好在终端中进行，直接复制可能会有权限问题）这时应该就可以通过'sudo matlab'打开Matlab软件了，打开后的界面如下：

![这里写图片描述](http://img.blog.csdn.net/20170823224755869?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

2. 安装Matlab支持包'sudo apt-get install matlab-support'。中间可选使用这款软件的用户以及重命名GCC库，原文教程中说可以忽略。我把当前用户作为了使用这款产品的用户。

3. 为了避免每次都用root权限打开matlab，通过'sudo chown username -R ~/.matlab'改变权限。最终直接在终端输入'matlab'就可以打开Matlab了，至此完成了Matlab在Ubuntu下的安装。