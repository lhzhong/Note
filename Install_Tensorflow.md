## **用Anaconda方法安装tensorflow**

> 注：不开辟另外的计算空间也能直接安装，直接跳到3步骤即可实现

#### 1. 建立一个conda计算环境
`$ conda create -n tensorflow python=2.7`
#### 2.激活环境
`$ source activate tensorflow`
#### 3.安装tensorflow

1）去清华镜像网站选择对应版本（操作系统，Python版本，CPU版本还是GPU版本）

  [清华镜像网站](https://mirrors.tuna.tsinghua.edu.cn/help/tensorflow/)

2）复制相应命令进行安装

例如：
```
(tensorflow)$ pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ https://mirrors.tuna.tsinghua.edu.cn/tensorflow/linux/gpu/
```

#### 4.在conda的tensorflow环境下安装jupyter
```
(tensorflow)$ conda install ipython  #安装notebook
(tensorflow)$ conda install jupyter  #安装jupyter
(tensorflow)$ conda install spyder  #安装spyder
(tensorflow)$ conda install --channel https://conda.anaconda.org/menpo opencv #安装opencv2
(tensorflow)$ conda install --channel https://conda.anaconda.org/menpo opencv3 #安装opencv3
```

#### 5.从conda环境中退出
(tensorflow)$ source deactivate

#### 6.windows下安装tensorflow

cpu:

`pip install --upgrade --ignore-installed tensorflo`

gpu:

`pip install --upgrade --ignore-installed tensorflow-gpu`
