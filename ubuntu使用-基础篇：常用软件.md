---
title: ubuntu使用-基础篇：常用软件
date: 2017-10-31 19:10:00
tags: ubuntu 常用软件
---
#1.谷歌浏览器：#
<!--more-->
1. 添加源：`sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/`
1. 导入谷歌软件公钥：`wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -`
1. 更新源：`sudo apt-get update`
1. 安装谷歌浏览器：`sudo apt-get install google-chrome-stable`
1. 安装完之后可以卸载自带的火狐浏览器：`sudo apt-get autoremove firefox firefox-branding firefox-gnome-support ubufox `
1. 配置谷歌浏览器（翻墙）：下载谷歌hosts文件，替换/etc/下的hosts文件，注意用sudo用户替换。

#2.搜狗输入法：#
1. 在[此处](http://pinyin.sogou.com/linux/)下载相关的deb文件，使用下面命令安装：`sudo dpkg -i sogoupinyin_2.1.0.0086_amd64.deb`，可能会安装不成功，缺少依赖项，使用` sudo apt-get install -f `安装依赖项，然后重新安装。
2. 配置搜狗输入法：重新启动电脑使搜狗输入法生效，打开fcitx进行配置搜狗输入法，同时也可以设置搜狗输入法的皮肤等。

#3.wps：#
3. 卸载ubuntu自带的libreoffice：`sudo apt-get purge libreoffice?`，通配符？表示卸载所有相关的东西。
3. 下载ubuntu版本的wps：[下载地址](http://community.wps.cn/download/)，下载完成之后安装：`sudo dpkg -i wps-office_10.1.0.5672-a21_amd64.deb `，安装过程中可能会出现缺少依赖项的问题，使用`sudo apt-get install -f `进行处理，处理完成后再进行安装。
3. 后期处理：安装完的wps会出现缺失字体的情况，下载对应的字体，将其复制到/usr/share/fonts中，`sudo cp * /usr/share/fonts`。

#4.ubuntu版本网易云音乐：#
4. 下载ubuntu版本的网易云音乐：[下载地址](http://music.163.com/#/download)。
4. 安装：`sudo dpkg -i netease-cloud-music_1.0.0_amd64_ubuntu16.04.deb `，出现缺少依赖项的时候用`sudo apt-get install -f`处理一下。

#5.ubuntu版本迅雷：#
5. 下载ubuntu版本迅雷xware：[下载地址](http://download.csdn.net/download/ghan_/9944727)。
5. 安装：`sudo dpkg -i xware-desktop_0.13.20160328_amd64.deb `，过程中使用`sudo apt-get install -f`处理再进行安装。
5. 配置xware：安装完成之后打开xware，依次打开文件->设置->启动与登录，xwared托管选择systemed托管，ETM随xwared启动；在挂载中增加一个挂载点。然后重启电脑，xware生效，进去点击激活就可以使用xware了。

#6.unity-tweak-tool#
调整 Unity 桌面环境，还是推荐使用Unity Tweak Tool，这是一个非常好用的 Unity 图形化管理工具，可以修改工作区数量、热区等。使用`sudo apt-get install unity-tweak-tool`安装。

#7.为知笔记#
为知笔记是linux下的一款强大的笔记软件，使用下面的命令进行安装。
```
sudo add-apt-repository ppa:wiznote-team
sudo apt-get update
sudo apt-get install wiznote

```

#8.其他软件#

1. shutter：ubuntu中比较好用的截图工具：`sudo apt-get install shutter`

1. git：程序员必备：`sudo apt-get install git`

1. vim：编辑器之神：`sudo apt-get install vim-gtk` vim配置见另一篇博客：