---
title: 在Visual C++ 2013 工程中使用 Matlab2014b 提供的图形引擎进行绘图的详细过程。
date: 2017-10-31 12:30:00
tags: vs2013 matlab 混合编程
---
在Visual C++ 2013 工程中使用 Matlab2014b 提供的图形引擎进行绘图的详细过程。
<!-- more --> 
在编程过程中有时候会遇到在c++中调用matlab，由于matlab强大的图像处理能力和科学计算能力，在c++中适当的调用matlab能够极大的提高编程效率，尤其是在处理图像和科学计算的时候。
最近两天研究这方面的配置花了好长时间，终于在使用多种方法之后得到了解决，下面将自己的配置过程以及遇到的一些问题写下了，方便自己以后查看，同时也希望能帮到和我一样遇到类似困难的朋友！
# 前期准备：
下载vs2013和matlab2014b（版本有差异应该不影响后续），并且安装。下载地址请自行google。
# 开始配置：
1. 打开vs2013，新建一个win32控制台应用程序，名称，位置随意。
1. 在项目上右键点击属性，打开项目属性页，点击配置属性。
1. 点击右上角的配置管理器  
![这里写图片描述](http://img.blog.csdn.net/20161118194639938)
1. 新建一个活动解决方案  
![这里写图片描述](http://img.blog.csdn.net/20161118194755377)
1. 选择x64位活动平台，点击确认。该步骤将32位平台转换为64为平台，原因是vs2013初始只能创建32位活动平台，如果电脑上装的是64位的matlab，就必须使用64位的平台，32位的matlab的朋友请自行忽视这一步。
1. 点击vc++目录打开相应的窗口，设置可执行文件目录，包含目录，库目录三个目录。  
![这里写图片描述](http://img.blog.csdn.net/20161118195709009)  
设置分别如下：(注意请自行修改相关路径，并且注意后面用;隔开)
可执行文件目录：D:\Hosea_Pro\MATLAB\extern\include\win64;
包含目录：D:\Hosea_Pro\MATLAB\bin\win64;
库目录：D:\Hosea_Pro\MATLAB\extern\lib\win64\microsoft;
1. 点击连接器下的输入，在附加依赖项中输入libmat.lib;libeng.lib;libmx.lib;点击确定完成相关配置。  
![这里写图片描述](http://img.blog.csdn.net/20161118200102921)
1. 新建一个cpp文件进行测试：测试代码来借鉴于网上一位博主的代码。
```
#include<cstdlib>
#include <cstdio>
#include<cstring>
#include"engine.h"

const int BUFFER_SIZE = 1024;
char buffer[BUFFER_SIZE];

void test()
{
	Engine* ep;
	mxArray *x1 = NULL;
	mxArray *y1 = NULL;
	if ((ep = engOpen("")) == NULL)
	{
		printf("Engine Fail");
	}
	engOutputBuffer(ep, buffer, BUFFER_SIZE);
	printf("Init Success");

	double x[5] = { 1.0, 2.5, 3.7, 4.4, 5.1 };
	double y[5] = { 3.3, 4.7, 9.6, 15.6, 21.3 };
	x1 = mxCreateDoubleMatrix(1, 5, mxREAL);
	y1 = mxCreateDoubleMatrix(1, 5, mxREAL);

	memcpy((void *)mxGetPr(x1), (void *)x, sizeof(x));
	memcpy((void *)mxGetPr(y1), (void *)y, sizeof(y));

	engPutVariable(ep, "x", x1);
	engPutVariable(ep, "y", y1);

	engEvalString(ep, "plot(x,y)");
	getchar();
	engClose(ep);
}

int main()
{
	test();
}
```
生成解决方案，运行，结果如下。  
![这里写图片描述](http://img.blog.csdn.net/20161118200817321)  
可以看到，vs2013调用matlab完美成功。
1. 基本上改了平台，填了目录，填了库名，就可以万事大吉了。但是有时候往往还是会有各种破事，比如提示libeng.dll找不到啊之类的。这时候呢，可以通过修改环境变量的方式来解决这个问题。D:\Hosea_Pro\MATLAB\R2014b\bin\win64; 把原来可执行程序的目录加入到系统的PATH环境变量中，然后记得重启。。。。就可以解决问题了
# 遇到的问题：
第一个遇到的问题就是平台不合适的问题，这个问题也是困扰我时间最长的一个问题，刚开始的时候没有注意的这个问题，所以出现了许多无法解析外部符号的问题：  
![这里写图片描述](http://img.blog.csdn.net/20161118202438362)  
[主要参考自(http://www.cnblogs.com/Vonng/p/4232586.html)](http://www.cnblogs.com/Vonng/p/4232586.html)