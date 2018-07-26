## **用Anaconda方法安装tensorflow**

根据tensoflow的官网说明，tensorflow的安装有四种方法，但这里主要采用其中两种方法进行安装  
* 方法一：直接安装
* 方法二：用anaconda开辟一个虚拟空间进行安装

### 一、直接安装

由于在国内不挂vpn无法登陆tensorflow官网，所以如果采用官网安装说明可能会安装不成功。国内清华有个镜像网站，通过替换镜像可以方便进行安装，只要进行清华镜像网站找到相应版本进行安装即可

**1）去清华镜像网站选择对应版本（操作系统，Python版本，CPU版本还是GPU版本）**

  [清华镜像网站](https://mirrors.tuna.tsinghua.edu.cn/help/tensorflow/)

**2）复制相应命令进行安装**

例如：
```
(tensorflow)$ pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ https://mirrors.tuna.tsinghua.edu.cn/tensorflow/linux/gpu/
```

### 二、用Anaconda方法安装tensorflow

在conda环境中安装tensorflow的好处是可以便捷的管理tensorflow的依赖包。分为两个步骤：  
* 激活上一步建立的名为tensorflow的conda环境  
* 用conda或者pip工具安装Tensorflow  

**1）建立一个conda计算环境**  
```
$ conda create -n tensorflow python=2.7  # python 2.7版本的
$ conda create -n tensorflow python=3.5  # python 3.5版本的
```

**2）激活环境**  
`$ source activate tensorflow`

**3）安装tensorflow**  
由于按官网说明直接安装没有翻墙安装会不成功，因此推荐还是用第一种方法进行tensorflow的安装

**4）在conda的tensorflow环境下安装jupyter**  
```
(tensorflow)$ conda install ipython  #安装notebook
(tensorflow)$ conda install jupyter  #安装jupyter
(tensorflow)$ conda install spyder  #安装spyder
```

**5.从conda环境中退出**  
`(tensorflow)$ source deactivate`

### 三、windows下安装tensorflow

cpu:

`pip install --upgrade --ignore-installed tensorflow`

gpu:

`pip install --upgrade --ignore-installed tensorflow-gpu`
