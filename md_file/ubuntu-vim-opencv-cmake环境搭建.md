---
title: ubuntu+vim+opencv+cmake环境搭建
date: 2017-10-31 16:00:00
tags: 
- ubuntu
- vim
- opencv
- cmake
categories: ubuntu
---
# 在ubuntu环境下搭建opencv开发环境
<!-- more -->
最近由于学习需要，要用到opencv，所以就在ubuntu下搭建了opencv环境，由于为了更好的学习基础，所以没有使用集成开发环境，而是在vim下开发。本次搭建过程在ubuntu16.04系统中搭建，opencv版本为3.2.0。

在安装OpenCV之前，需要进行一系列准备工作。

# 一.安装编译器  
首先查看自己系统中编译器的版本：
`ghan@Ghan:~$ gcc -v`
显示结果如下：gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.4) ，编译器完美支持，如果没有安装，请使用如下命令安装：
`ghan@Ghan:~$ sudo apt-get install build-essential`

# 二.安装cmake编译工具：
用于opencv开发的话，cmake版本要为2.6以上，我使用的版本为3.5.1，直接可以使用`cmake --version`查看cmake的版本，如未安装的话先到官网[https://cmake.org/download/](https://cmake.org/download/) 下载tar.gz包，然后解压之后在终端中进入该目录，然后执行一下命令：

```
ghan@Ghan:~/Downloads/cmake-3.5.1$ ./bootstrap
ghan@Ghan:~/Downloads/cmake-3.5.1$ make
ghan@Ghan:~/Downloads/cmake-3.5.1$ sudo make install
```
上面过程执行完之后可以再次查看一下是否安装成功。

# 三 安装Opencv
1. 安装OpenCV依赖库  
OpenCV会依赖许多库，所以要先安装这些依赖库，可以使用如下命令：
```
ghan@Ghan:~$ sudo apt-get install libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg8-dev libjpeg-dev libtiff5-dev libswscale-dev libjasper-dev
```
接着更新这些库：`ghan@Ghan:~$ sudo apt-get updata`

1. 安装OpenCV  
首先第一步时下载OpenCV的源代码，[http://opencv.org/opencv-3-2.html](http://opencv.org/opencv-3-2.html) 下载opencv-3.2.0.zip源代码包，然后将其解压，再进入到该解压目录，然后执行以下命令：  
```
ghan@Ghan:~/Downloads/opencv/opencv-3.2.0$ cmake .
ghan@Ghan:~/Downloads/opencv/opencv-3.2.0$ make
ghan@Ghan:~/Downloads/opencv/opencv-3.2.0$ sudo make install
```
该过程会消耗较长时间，另外如果中间有卡顿下载东西，请耐心等等，安装完成之后在/usr/local/lib目录下会看到许多*.so结尾的opencv文件，
同时在/usr/local/include目录下会看到opencv和opencv2文件夹，里面存放着opencv库的头文件。至此Opencv安装完成.
1. opencv配置  
第一步创建配置文件opencv.conf ` ghan@Ghan:~$ sudo vim /etc/ld.so.conf.d/opencv.conf `
第一次创建该文件时应该是空文件，向里面写入如下内容并保存退出：`/usr/local/lib` opencv中lib的目录  
接着执行以下命令，使该配置文件生效:`ghan@Ghan:~$ sudo ldconfig`
第二步配置环境变量bash.bashrc `ghan@Ghan:~$ sudo vim /etc/bash.bashrc `
在该文件的末尾添加以下内容：  
```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig/ 
export PKG_CONFIG_PATH
```
更新环境变量 `ghan@Ghan:~$ source /etc/bash.bashrc `
上面几个过程主要介绍了ubuntu中opencv的安装以及配置，下面介绍以下如何使用opencv。  

1. 测试opencv  
第一步：在相关目录下创建项目目录：
` ghan@Ghan:~/Documents/Code$ mkdir opencv`
在该目录下新建一个test.cpp文件` `

```
#include"iostream"
#include <opencv2/opencv.hpp>
using namespace std;
using namespace cv;                                                         
int main(int argc,char** argv){
    if(argc!=2){
        cout<<"image_path error!"<<endl;
        return -1;
    }
    Mat image=imread(argv[1],1);
    if(!image.data){
        cout<<"image error!"<<endl;
        return -1;
    }
    namedWindow("Image",WINDOW_AUTOSIZE);
    imshow("Image",image);
    waitKey(0);
    return 0;
}
```
接着在该目录下创建cmake编译文件
` ghan@Ghan:~/Documents/Code/opencv$ vim CMakeLists.txt`
向该文件中添加如下内容：
```
cmake_minimum_required(VERSION 2.8)
project(test)
find_package(OpenCV REQUIRED)
add_executable(test test.cpp)
target_link_libraries(test ${OpenCV_LIBS}) 
```
此时在该目录下存在以下的文件：
`CMakeLists.txt     lena.jpg     test.cpp `

第二步：编译
使用以下命令：

```
ghan@Ghan:~/Documents/Code/opencv$ cmake .
ghan@Ghan:~/Documents/Code/opencv$ make
```
然后进行运行
` ghan@Ghan:~/Documents/Code/opencv$ ./test lena.jpg `

最终完美运行。
