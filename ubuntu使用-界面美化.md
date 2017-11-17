---
title: ubuntu使用-界面美化
date: 2017-10-31 19:00:00
tags: ubuntu 界面美化
---
本篇介绍ubuntu中的界面美化，界面美化不仅能提升系统的颜值，同时对于系统的使用也会有一定的提升。
<!-- more -->

#1.字体#

ubuntu自带的字体不太好看，而且在终端中会出现字体堆叠的现象，所以采用文泉译微米黑字体替代，效果会比较好，毕竟是国产字体！


sudo apt-get install fonts-wqy-microhei
安装好字体之后在unity Tweak Tool中进行配置
![这里写图片描述](http://img.blog.csdn.net/20170822190817085?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

在字体中选择
![这里写图片描述](http://img.blog.csdn.net/20170822190832177?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#2.扁平化主题与图标#

###flatabulous扁平化主题###

使用以下命令安装：

sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme

###alatabulous配套的图标###

使用以下命令安装：

sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons

安装完之后在unity-tweak-tool中配置，安装完之后的效果如下：
![这里写图片描述](http://img.blog.csdn.net/20170822190854402?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvR2hhbl8=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


