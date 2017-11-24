---
title: ubuntu16.04安装shadowsocks-qt5
date: 2017-11-23 12:10:00
tags:
  - shadowsocks 翻墙 ubuntu
categories: tech
---
作为一个学习中的程序员，查wiki等，科学上网肯定是刚需。况且没有它很多东西都下不下来。我在windows环境下使用的是shadowsocks，那么在linux下也使用它。
<!--more-->
# 安装
这里我使用的是Qt5版本。安装过程如下： 
1. 首先打开终端（Ctrl+Alt+T） 
1. 然后分步运行以下三行命令：
    ```
    sudo add-apt-repository ppa:hzwhuang/ss-qt5 &&
    sudo apt-get update &&
    sudo apt-get install shadowsocks-qt5
    ```
  ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flrw9a5bisj20db0dx3z1.jpg)  
# 软件配置
  安装自己的情况填写下面的信息：  
  ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flruoybtb1j20970el3zk.jpg)
  填写完成后点击连接即可。
# 网络代理配置
网络代理配置如下：
1. 打开系统设置->网络->网络代理
1. 按照如下的信息填写即可：
  ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flruoygz5fj20ni0e1q3u.jpg)
# 浏览器配置
1. 下载SwitchyOmega插件，[github链接]，(https://github.com/FelisCatus/SwitchyOmega/releases) [个人网盘](https://www.nextcloud.ghan.top/index.php/s/i1JN6GT3ukuxYKR)
1. 按下图所示直接导入配置文件，[配置文件链接](http://fybbs.u.qiniudn.com/OmegaOptions1080.bak)
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flrwa3289fj20v10hh0v7.jpg)
1. 导入成功的界面：
![](https://ws1.sinaimg.cn/large/c2894cd5gy1flrxfvb4ogj20z90h1q4e.jpg)
然后就可以愉快的翻墙了。