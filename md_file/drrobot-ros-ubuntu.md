---
title: ubuntu环境下搭建ROS系统并用于DrRobot Jaguar4x4机器人开发
date: 2018-2-1 19:04:00
tags:
  - ubuntu ROS Drrobot
categories: tech
---
* 本文介绍了在ubuntu操作系统下搭建ROS机器人系统，并且用于Jaguar4x4_2014机器人开发。  
<!--more-->
# 前期准备：
* 安装ubuntu：由于网上的资料大部分都是在ubuntu12.04下编译的，因此本文使用的ubuntu系统也是12.04。
* ROS系统，直接戳[ros官网](!http://wiki.ros.org/)有详细的介绍，也可以观看[实验楼](!https://www.shiyanlou.com/courses/854)观看文档介绍，看完基本上会对ROS有一个比较直观的理解。本博文也是在上面两个地方进行总结而来。
# 环境配置：
## drrobot Jaguar4x4机器人网络配置:
### 无线路由器设置  
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/1.jpg?raw=true)
### 硬件默认设置
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/2.jpg?raw=true)  
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/3.jpg?raw=true)  
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/4.jpg?raw=true)  
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/5.jpg?raw=true)  
### ubuntu系统配置
#### 连接机器人
打开机器人，等待1分钟左右搜索机器人局域网DRIJaguar，密码：drrobotdrrobot，**连接之后修改本机IP地址为：192.168.0.104，子网掩码为：255.255.255.0**即可，至此机器人已经连接成功。
#### 软件配置 
- 版本选择： 
首先明确Ubunut系统版本和ROS系统版本要一致，不然会出错，对应如下图：  
![](https://github.com/Hosea1/markdown_file/blob/master/md_image/drrobot_ros_ubuntu/6.jpg?raw=true)  
- 安装ROS机器人系统： 
本人使用的ubuntu版本为12.04 LTS，因此选择ROS版本为Hydeo，下面进行安装：
    - 添加源：`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'`
- 配置
