# Some tricks about tensorflow

* **Download pretrained model**

  https://github.com/tensorflow/models/tree/master/research/slim#Pretrained

* **The value of the training loss don't descent**

  May be you can change your learning rate.

* **See the version of Tensorflow**
```
$ python
import tensorflow as tf
tf.__version__
```

* **python判断后缀是否为图片**
```
fileName1='pic.jpg'
if fileName1.endswith(('.gif', '.jpg', '.png')):
    print '这是一张图片'
else:
    print '这不是一张图片'
```

