### 电脑环境和软件版本

    | software/hardware |  Configuration  |
    | ----------------- |-----------------| 
    | GPU               | GTX1080         |
    | Linux             | 16.04(LTS)64    | 
    | python            | Anaconda2       | 
    | cuda              | 8.0             |
    | cudnn             | 8.0             |
    | drive             | x86_64-381.22   | 


## 一、安装Ubuntu（我的版本16.04）

用UltraISO做一个系统盘，系统安装按引导进行。
> 注：在进入ubuntu安装界面时，会出现黑屏现象，需要进行一定修改。
进入grub画面后（如果进不了grub，开机时按住shift不放），按"e"进入编辑开机指令模式，在“quite splash”后加上nomodeset，按F10保存启动

## 二、安装Nvidia驱动（我的版本NVIDIA-Linux-x86_64-381.22）

#### 1.下载驱动（选择自己需要的版本和驱动）
NVIDIA官网下载网址： http://www.nvidia.cn/Download/index.aspx?lang=cn

#### 2.进入字符界面，按Ctrl+Alt+F1，删除旧的驱动
`$ sudo apt-get purge nvidia*`

#### 3.禁用自带的nouveau nvidia驱动 （很重要！）

1）创建文件

`$ sudo vim /etc/modprobe.d/blacklist-nouveau.conf`

2）在文件中添加

```
blacklist nouveau 
options nouveau modeset=0
```

3）更新

`$ sudo update-initramfs -u`

#### 4.安装自己驱动

1）重启系统

`$ sudo reboot`

2）进入字符界面

Ctrl+Alt+F1

3）关闭X-Window

`$ sudo service lightdm stop`

4）切换到驱动所在目录

`$ cd {驱动所在目录} `

5）增加权限并安装
```
$ sudo chmod 777 NVIDIA-Linux-x86_64-381.22.run
$ sudo ./NVIDIA-Linux-x86_64-381.22.run
```
6）安装完成后执行

$ sudo service lightdm start

#### 5.测试检验是否安装成功

`$ nvidia-smi`

#### 6.问题

有时会出现下一次进入界面时，界面一直停留在锁屏界面，尽管密码输入正确

**解决**：把驱动先卸了再重装

1）进入字符界面

Ctrl+Alt+F1

2）关闭X-Window

`$ sudo service lightdm stop`

3）$cd {驱动所在目录}并执行

`$ sudo ./NVIDIA-Linux-x86_64-381.22.run --uninstall`

4）重新安装驱动

```
$ sudo ./NVIDIA-Linux-x86_64-381.22.run
$ sudo service lightdm start
```

## 三、系统软件源设置并设置

1）系统设置(system settings)---->软件与更新(software & update)----->选择Ubuntu软件（Ubuntu software)选项卡，改变系统软件源为阿里的源。

2）更新列表

```
$ sudo apt-get update
$ sudo apt-get upgrade
```

## 四、安装Anaconda2（我的版本2.7）

#### 1.下载Anaconda（我下的2.7版本的）

#### 2.cd {Anaconda2所在目录}并执行 

`$ bash Anaconda2-2.4.1-Linux-x86_64.sh`

* 在安装的过程中，会问你安装路径，直接回车默认就可以了。
* 有个地方问你是否将anaconda安装路径加入到环境变量（.bashrc)中，这个一定要输入yes。
* 安装成功后，会有当前用户根目录下生成一个anaconda2的文件夹，里面就是安装好的内容。

#### 3.设置环境变量

`$ sudo gedit /etc/profile`

添加内容：

`export PATH=/home/zhong/anaconda2/bin:$PATH`

使环境变量立即生效：

`$ source /etc/profile`

#### 4.在终端输入python命令，如果没报错，出现Anaconda2版本，说明anaconda2安装完毕。

## 五、安装CUDA（我的版本8.0）

一定要搞清楚你自己的显卡要装什么版本的驱动，以及支持的cuda版本，
Ubuntu16.04需要的gcc版本为5.3.1，而当Ubuntu16.04安装好之后，系统自带的gcc版本为5.4,所以gcc要重新安装
![](https://github.com/lhzhong/iNote/blob/master/pic/gcc.png?raw=true)

#### 1.GCC降级

1）查看gcc版本

`$ gcc -v`

如果版本是5.3.1以下的就不用降级了，否则要降级gcc

2）下载gcc

http://pan.baidu.com/s/1hrBhF84 密码：98ix

3）解压，进入gcc目录，下载依赖项

```
$ sudo tar -zxvf gcc-5.3.0.tar.gz 
$ cd gcc-5.3.0/  
$ sudo ./contrib/download_prerequisites 
```

4）新建文件夹，生成makefile文件

```
$ sudo mkdir build
$ cd build/
$ sudo ../configure --enable-checking=release --enable-languages=c,c++ --disable-multilib
```

5）编译安装

```
$ sudo make -j8  
$ sudo make install 
```

6）查看是否安装成功

`$ gcc --version`

#### 2.安装cuda

1）cd到cuda下载目录

2）运行cuda安装

`$ sudo ./cuda_8.0.44_linux.run`

3）进入声明和安装指导界面
* 声明界面可以连续按Ctr+f向下阅读直到结尾，也可以按Ctr+C跳过阅读。
* 有个让你选择是否安装nvidia367驱动时，选择否：（Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 367.48?）
因为前面我们已经安装过了，所以这里不要选择安装。

4）安装一些依赖库

`$ sudo apt-get install freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libgl1-mesa-glx libglu1-mesa libglu1-mesa-dev`

5）打开.bashrc文件进行配置

`$ sudo gedit ~/.bashrc`

添加内容：

```
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
export CUDA_HOME=/usr/local/cuda
 ```

6）设置环境变量

`$ sudo gedit /etc/profile`

添加内容：

`export PATH=/usr/local/cuda/bin:$PATH `

使环境变量立即生效：

`$ source /etc/profile`

7）创建链接文件

`$ sudo gedit /etc/ld.so.conf.d/cuda.conf`

添加内容：

`/usr/local/cuda/lib64 `

使链接立即生效：

`$ sudo ldconfig `

8）测试

```
$ cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery
$ make
$ sudo ./deviceQuery
```

如果显示一些关于GPU的信息，则说明安装成功。
> 注：查看版本：`$ nvcc –V`

## 六、安装cuDNN（我的版本8.0）

cuDNN是GPU加速计算深层神经网络的库

#### 1.下载cuDNN

#### 2.解压

`$ tar -zxvf ./cudnn-8.0-linux-x64-v5.0.tgz`

#### 3.进入cuDNN5.0解压之后的include目录，执行：

```
$ cd cuda/include
$ sudo cp cudnn.h /usr/local/cuda/include  #复制头文件
```

4.将进入lib64目录下的动态文件进行复制和链接：

```
$ cd ../lib64
$ sudo cp lib* /usr/local/cuda/lib64/
$ cd /usr/local/cuda/lib64/
$ sudo chmod +r libcudnn.so.6.0.5
$ sudo ln -sf libcudnn.so.6.0.6 libcudnn.so.6
$ sudo ln -sf libcudnn.so.6 libcudnn.so
$ sudo ldconfig
```

## 七、安装opencv（我的版本2.4.9）

#### 1.下载opencv

http://pan.baidu.com/s/1qXD9l60 密码：yn62

#### 2.安装必要的组件

```
$ sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libdc1394-22-dev libatlas-base-dev gfortran
```

#### 3.解压

`$ unzip opencv2.4.9`

#### 4.安装

```
$ cd opencv2.4.9
$ mkdir build
$ cd build
$ sudo apt-get install cmake
$ sudo cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local -D CUDA_GENERATION=Kepler　..
$ sudo make -j8
$ sudo make install
```

#### 5.错误集锦

* **错误1：**

> nvcc fatal:Unsupported gpu architecture 'compute_11'

**解决**： 在cmake 命令添加：`-D CUDA_GENERATION=Kepler`

* **错误2：**

> /home/lingck/opencv-2.4.9/modules/gpu/src/nvidia/core/NCVPixelOperations.hpp(129): error: a storage class is not allowed in an explicit specialization

**解决**： 需要使用下载NCVPixelOperations.hpp替换掉opencv2.4.9内的文件， 重新build。 

http://pan.baidu.com/s/1jIejKY6 密码;rsrq

NCVPixelOperations.hpp所在目录为：`（编译OpenCV的路径）/modules/gpu/src/nvidia/core`

* **错误3：**

> make[2]: *** [modules/gpu/CMakeFiles/opencv_gpu.dir/src/graphcuts.cpp.o]

**解决**：打开`/opencv/modules/cudalegacy/src/graphcuts.cpp`文件

把graphcuts.cpp里面的

`if !defined (HAVE_CUDA) || defined (CUDA_DISABLER)`

改为

`if !defined (HAVE_CUDA) || defined (CUDA_DISABLER) || (CUDART_VERSION >= 8000)`

* **错误4：**

> make[2]: *** [modules/videoio/CMakeFiles/opencv_videoio.dir/src/cap_ffmpeg.cpp.o] Error 1

> make[2]: *** Waiting for unfinished jobs....

**解决**：跳过ffmpeg编译，在cmake 命令添加：`-D WITH_FFMPEG=0`

更多错误及解决：

https://stackoverflow.com/questions/31663498/opencv-3-0-0-make-error-with-ffmpeg

http://blog.csdn.net/hongbin_xu/article/details/75807940

http://blog.csdn.net/qq_14839543/article/details/73293370

#### 7.环境变量配置

1）创建opencv.conf，设置lib路径

`$ sudo gedit /etc/ld.so.conf.d/opencv.conf`

添加内容：

`/usr/local/lib`

使环境变量立即生效：

`$ sudo ldconfig`

2)打开.bashrc文件进行配置

`$ sudo gedit /etc/bash.bashrc`

添加内容：

`export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH`

#### 8.测试

在终端下输入python，然后`import cv2`,不报错即安装成功

**问题**：在python下执行`import cv2`，报错`ImportError: No module named cv2`

**解决**：在anaconda安装文件夹下建立cv2.so的软连接

```
$ sudo cp /home/zhong/Downloads/opencv-2.4.9/build/lib/cv2.so /usr/local/lib/python2.7/site-packages
$ sudo ln -s /usr/local/lib/python2.7/site-packages/cv2.so /home/zhong/anaconda2/lib/python2.7/site-packages/
```

> 注：以上是opencv源码安装，其实也可以在acaconda下直接安装opencv
```
替换清华源
$ conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
$ conda config --set show_channel_urls yes
$ conda install --channel https://conda.anaconda.org/menpo opencv3
```

## 八、安装MATLAB（我的版本MATLAB2014A）

> 安装时需要断网

#### 1.下载Matlab安装 

http://pan.baidu.com/s/1o7LK9gY 密码：eim8

#### 2.安装rar

`$ sudo apt-get install rar`

#### 3.解压下载的Matlab压缩文件（或选中两个压缩文件右击解压到当前文件夹）

`$ rar z MATHWORKS_R2014A.part1.rar`

解压后会得到一个镜像文件 MATHWORKS_R2014A.iso

#### 4.新建挂载文件夹

`$ mkdir matlab`

#### 5.切换到镜像所在文件夹，将MATHWORKS_R2014A.iso挂在到matlab/上

`$ sudo mount -o loop MATHWORKS_R2014A.iso ./matlab/`

#### 6.切换到matlab目录，进行安装

```
$ cd ~/matlab
$ sudo ./install
```

#### 7.安装

选择`"install manually without using the internet"`项进行安装

输入"file installation key"：使用crack文件下readme.txt文件中的序列号进行安装`(12345-67890-12345-67890)`

> 注：在create symbolic links to MATLAB scripts in页面一定把框里的勾打上，这样就能在安装完后在终端启动matlab

### 8.安装完成后使用crack下的 license进行激活,激活文件在Crack目录下

### 9.将crack文件夹下的`libmwservices.so` copy到`/usr/local/MATLAB/R2014A/bin/glnxa6`

`$ sudo cp ~/Matlab/Crack/Linux/libmwservices.so /usr/local/MATLAB/R2014A/bin/glnxa6`

#### 10.启动matlab
`$ matlab`

## 九、安装Caffe

#### 1.安装依赖包

```
$ sudo apt-get install libatlas-base-dev libprotobuf-dev libleveldb-dev libsnappy-dev libboost-all-dev libhdf5-serial-dev libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler
```

#### 2.下载源码

```
$ sudo apt-get install git
$ git clone https://github.com/bvlc/caffe.git
```

#### 3.修改 Makefile.config

```
$ cd caffe /
$ cp Makefile.config.example Makefile.config
$ gedit Makefile.config 
```

*Makefile.config文件*

https://pan.baidu.com/s/1rCXzD8XnToKRGJ5z3_VowA  密码：smsx


#### 4.设置环境变量

`$ sudo gedit /etc/profile`

添加内容：

`export PYTHONPATH=/home/zhong/caffe/python:$PYTHONPATH`

使环境变量立即生效：

`$ source /etc/profile`

#### 5.编译并检测

```
$ make -j8  
$ make test -j8
$ make runtest
```

#### 5.配置pycaffe

1)更新protobuf

`$ conda install protobuf`

2)编译

```
$ make pycaffe
$ make test -j8
$ python
```

3）测试

`$ python`

`>>import caffe`

若无报错，则成功。


## 十、参考

http://blog.csdn.net/leijiezhang/article/details/53688157

http://www.cnblogs.com/go-better/p/7161006.html

http://blog.csdn.net/liuxiaoheng1992/article/details/54588444




