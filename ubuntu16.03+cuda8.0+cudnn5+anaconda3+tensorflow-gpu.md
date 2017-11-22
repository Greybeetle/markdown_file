---
title: ubuntu16.03+cuda8.0+cudnn6+anaconda3+tensorflow-gpu
date: 2017-11-21 16:10:00
tags:
  - tensorflow-gpu
  - ubuntu
categories: 环境搭建
---
本文介绍了在ubuntu16.03下搭建深度学习库tensorflow的过程，同时使用nvidia显卡加速tensorflow的运行。
<!---more--->
# 安装前的准备
下载相关的软件：  
1. ubuntu16.04：系统，必备，下载玩安装，不会安装的请自行google！
1. cuda8.0：本人使用的cuda显卡驱动版本为8.0，也试过9.0的版本，发现这个版本兼容性最好！
1. cudnn6：cudnn6和cuda8.0的依赖关系较好
1. anaconda3：python3的版本，看自己喜好
1. TensorFlow-gpu
1. 安装一些依赖项：使用如下命令：
    ```
    sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler && 
    sudo apt-get install --no-install-recommends libboost-all-dev && 
    sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler && 
    sudo apt-get install --no-install-recommends libboost-all-dev && 
    sudo apt-get install python-skimage ipython python-pil python-h5py ipython python-gflags python-yaml && 
    sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
    ```
# cuda8.0安装过程
1. 在系统设置->软件和更新->附加驱动中，选择推荐的驱动。
1. 下载好cuda8.0，在终端中进行安装`sudo ./cuda_8.0.61_375.26_linux.run`，然后会出现一大堆的信息，按`ctrl+c`跳过即可，然后根据提示选择安装，应该注意的是不要安装显卡驱动，因为前面已经安装好了。
1. 安装成功之后，在终端输入`nvidia-smi`，显示如下信息即表示安装成功：  
    ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flpprhx0vzj20kc0bugms.jpg)
1. 如果出现错误，请尝试一下步骤：  
    * 在终端中输入`gedit ~/.bashrc`
    * 在打开的文件中输入：  
    ```
    export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    export CUDA_HOME=/usr/local/cuda
    ```
    * 保存并关闭文件，在终端中输入`source ~/.bashrc`，使其生效。
    * 最后在终端继续输入`nvidia-smi`查看。
1. 查看显卡状态：  
    cuda samples测试运行，检测cuda是否顺利安装：  
    * 切换到NVIDIA_CUDA-8.0_Samples目录下，输入命令`make`进行编译，此过程较长（~喝个咖啡先~~）
    * 编译完成之后，新的二进制文件默认放在bin目录下，`cd bin/x86_64/linux/release && ./deviceQuery`，如果出现下图的信息，则表示cuda安装且配置成功。  
    ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flpqriomn3j20w00jvn19.jpg)
# cudnn安装
1. 下载cudnn：
1. cudnn的安装较简单，执行以下命令将文件复制即可：  
    ```
    tar xvzf cudnn-8.0-linux-x64-v6.0.tgz
    sudo cp cuda/include/cudnn.h /usr/local/cuda-8.0/include
    sudo cp cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64
    sudo chmod a+r /usr/local/cuda-8.0/include/cudnn.h /usr/local/cuda-8.0/lib64/libcudnn*
    ```
    至此cudnn安装完毕。
# anaconda安装
1. 下载anaconda3.*.sh
1. 安装anaconda，`bash anaconda3.*.sh`按照自己的意愿进行安装。
1. 安装成功后输入`conda -V`，显示版本号即表示安装成功。
1. conda 常用命令：
    * `conda create --name tf-gpu python=3`：创建conda虚拟环境，名字是tf-gpu，python版本为3。
    * `conda info -e`：查看当前的conda虚拟环境。
    * `conda remove --name tf-gpu --all`：删除一个虚拟环境。
1. 创建conda虚拟环境完成之后，使用`source activate tf-gpu`激活此环境。
## tensorflow-gpu安装
在激活的tf-gpu环境中安装tensorflow。
1. 配置清华镜像：国内由于被墙的原因，tensorflow，matplotlib等包下载速度奇慢，所幸可以配置第三方镜像：终端中执行
    ```
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --set show_channel_urls yes
    ```
    执行完之后，前往当前用户目录下，查看是否出现一个.condarc的文件，打开之后，正常的情况下内容为：
    ```
    channels:
    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    - defaults
    show_channel_urls: true
    ```
1. pip安装tensorflow：`pip install tensorflow-gpu`    
1. 后续更新  
    * ***配置了清华镜像之后，发现还是无法安装tensorflow-gpu，直接用pip install tensorflow-gpu安装提示安装的版本为tensorflow_gpu-1.4.0-cp36-cp36m-manylinux1_x86_64.whl，但是去清华的镜像里面发现当时这个版本还没有更新，因此考虑用阿里镜像，但是阿里镜像和清华镜像配置不太一样。这种情况下我的办法是直接通过pip获取要安装的版本号（即版本名称），然后去阿里的镜像网站`http://mirrors.aliyun.com/pypi/simple/`找到相应的版本进行离线安装。安装命令如下：在激活的tf-gpu中将目录切换到tensorflow所在的文件夹`pip install tensorflow*`即可***
    * ***版本问题：考虑到python3.6还是会出现一些问题，所以在后面重新创建了一个虚拟环境，`conda create --name=tf-gpu python=3.5`***
1. 安装成功后`conda list`可以看到下面的信息：  
    ![](https://ws1.sinaimg.cn/large/c2894cd5gy1flpt66kz8aj20kz0ecq56.jpg)
1. `source deactivate&&source activate tf-gpu`重新启动虚拟环境，然后运行`python`，在python环境中输入以下代码测试：
```
import tensorflow as tf
a=tf.constant(1)
s=tf.Session()
b=s.run(a)
print(b)
```
最终的结果显示为1，正确的话tensorflow安装成功。
## 其他安装(以下安装都在虚拟环境中进行)
1. jupyter notebook安装：`pip install jupyter notebook`，个人常用的jupyter配置如下：
    1. 修改jupyter工作目录：`jupyter notebook --generate-config`生成jupyter notebook配置文件。然后修改#c.NotebookApp.notebook_dir=''为c.NotebookApp.notebook_dir='指定的路径'
    1. 修改jupyter_contrib_nbextensions，`pip install jupyter_contrib_nbextensions`,配置nbextension，`jupyter contrib nbextension install --user`
1. matplotlib：`pip install matplotlib`：经测试，安装过程极慢，因此选择使用本地安装。
***
到此为止，整个环境都已经搭建好了，可以愉快的coding了，下面给出一些软件的下载地址，仅供参考（以表格的形式给出，只给出一些下载速度慢的python包，别的基本上都可以直接使用`pip install *` 安装）：  
|       文件名称        |       官方网站       |        第三方镜像          |         个人网盘        |
|----------------------|:--------------------|---------------------------:|-----------------------:|
|cuda|[官方下载](https://developer.nvidia.com/cuda-downloads)|[清华镜像] [阿里镜像]|[个人网盘-cuda8]()|
|cudnn|[官方下载](https://developer.nvidia.com/cudnn)|not find|[个人网盘-cudnn6]()|
|anaconda|[官方下载](https://www.anaconda.com/download/)|[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)|[个人网盘-anaconda3]()|
|tensorflow|无法访问|[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/tensorflow/)|[个人网盘-tensorflow_gpu]()|
|matplotlib|[官方下载](https://pypi.python.org/pypi/matplotlib)|[清华镜像] [阿里镜像]|[个人网盘]()|
