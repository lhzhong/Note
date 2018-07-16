### 1.下载Anaconda（推荐下python3版本的）
清华镜像网站下载对应版本

[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)

### 2.在下载的Anaconda目录下执行
`$  bash Anaconda2-2.4.1-Linux-x86_64.sh`

* 在安装的过程中，会问你安装路径，直接回车默认就可以了
* 跳过阅读可以按Ctrl+C
* 有个地方问你是否将anaconda安装路径加入到环境变量（.bashrc)中，这个一定要输入yes
* 安装成功后，会有当前用户根目录下生成一个anaconda2的文件夹，里面就是安装好的内容

### 3.修改环境变量
* 在终端输入

`$ sudo vi /etc/profile`

* 在profile文件末尾添加

`export PATH=/home/zhong/anaconda2/bin:$PATH`

> 将`"/home/zhong/anaconda2/bin"`替换为你实际的安装路径。保存。

### 4.使环境变量生效
`$ source /etc/profile`

### 5.用conda 安装package
`$ conda install xxx`

***

**问题：**

官方下载的Anaconda在安装package如果报如下错误

> Fetching package metadata ... CondaHTTPError: HTTP None None for url Elapsed: 
None An HTTP error occurred when trying to retrieve this URL. HTTP errors are often intermittent,
and a simple retry will get you on your way. xxxx````````

**原因：**

可能是conda config这个用的是默认的镜像元设置链接不上，因此我们要用别的镜像元。

**解决：**
*  添加Anaconda的TUNA镜像 

`$ conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`
* TUNA的help中镜像地址加有引号，需要去掉 # 设置搜索时显示通道地址
```
$ conda config --set show_channel_urls yes
$ conda config --show-source
```

* 把-default 默认设置删掉
`$ sudo vim ~/.condarc`

  进去把default那一行删掉就可以了
