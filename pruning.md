## 非结构性剪枝

#### LWC（2015）
阈值通过每一层参数的方差决定，剪枝后参数不可恢复，AleNet压缩9倍，VGG压缩13倍。

#### Deep Compression（ICLR 2016 best paper）
基于LWC，加入了权值量化和哈夫曼编码，AlenNet压缩35倍。

#### DNS（NIPS 2016）
针对LWC参数不可恢复，提出用splicing步骤恢复参数。主要通过对参数加掩模实现，对掩模进行更新决定参数是否裁剪。阈值通过权值绝对值的平均值设定，设置高阈值和低阈值，大于高阈值恢复权值，低于低阈值删除，中间保持现有状态。AlexNet压缩17.7倍。

#### 迭代硬阈值（2016）
通过在网络的损失函数中增加一个关于W的L0范式降低W的稀疏度，自己设定剪枝率。边训练边裁剪，先将认为不重要的值裁掉，再通过一个restore的过程将重要却被误裁的参数恢复回来。训练过程：先正常训练网络s1轮，然后选出W中数值最大的k个数，将剩下的值置为0，继续训练s2轮，仅更新非0的W，然后再将之前置为0的W放开进行更新，继续训练s1轮，这样反复直至训练完毕。

#### 彩票假设（ICLR2019）
将一个复杂网络的所有参数当作一个奖池，奖池中存在一组子参数所对应的子网络，单独训练该子网络，可以达到原始网络的测试精度。首先初始化网络，然后训练网络，接着在训练完的网络中剪掉给定剪枝率的参数，最后对未裁剪参数用最初的随机初始化参数进行训练。迭代以上过程，以产生中奖彩票。

这篇文章证明的是初始化方式更重要，用大网络同样的初始化方式可以在性能不会下降的情况下更快的训练这个小网络，但是随机初始化不能将这个网络训练到同样的性能。

同样ICLR另一篇文章证明最后的网络更重要，而随机初始化只要通过调参就能达到相同效果。

## 结构性剪枝

#### Structure Sparisity Learning（2015）
在损失函数中加上约束。用group Lasso Regularization约束不同结构，如filters, channels, filter shapes, depth of layers。

#### weight sum（ICLR2017）
对所有weight的绝对值求和，来作为该filter的评价指标。作者在裁剪的时候同样会考虑每一层对裁剪的敏感程度，作者会单独裁剪每一层来看裁剪后的准确率。对于裁剪较敏感的层，作者使用更小的裁剪力度，或者跳过这些层不进行裁剪。

#### network trimming（NIPS2016）
度量relu之后的结果的稀疏度。作者认为，在大型的深度学习网络中，大部分的神经元的激活都是趋向于零的，而这些激活为0的神经元是冗余的，将它们剔除可以大大降低模型的大小和运算量，而不会对模型的性能造成影响，于是作者定义了一个量APoZ（Average Percentage of Zeros）来衡量每一个filter中激活为0的值的数量，来作为评价一个filter是否重要的标准。

#### network slimming（ICCV2017）
利用BN层中的缩放因子γ，在训练过程当中来衡量channel的重要性加入损失函数中，将不重要的channel进行删减。将当前层的γ全都加起来，然后按从大到小的顺序排列，选取较大的那一部分，通常选取70%左右

#### Entropy-based Pruning（2017）
作者认为通过weight值的大小很难判定filter的重要性，通过这个来裁剪的话有可能裁掉一些有用的filter。因此提出了一种基于熵值的裁剪方式，利用熵值来判定filter的重要性。

作者将每一层的输出通过一个Global average Pooling将feature map转换为一个长度为c（filter数量）的向量，对于n张图像可以得到一个n*c的矩阵，对于每一个filter，将它分为m个bin，统计每个bin的概率，然后计算它的熵值，利用熵值来判定filter的重要性，再对不重要的filter进行裁剪。
```math
H_{j}=-\sum_{i=1}^{m} p_{i} \log p_{i}
```
裁剪是在把一轮迭代数据都输入后统计其熵后进行的。每裁剪完一层，通过少数几个迭代来恢复部分的性能，当所有层都裁剪完之后，再通过较多的迭代来恢复整体的性能

#### Taylor expansion（NIPS2016）
近似的求算对loss的影响力度。作者将裁剪问题当做一个组合优化问题：从众多的权重参数中选择一个最优的组合B，使得被裁剪的模型的代价函数的损失最小。
```math
\min _{\mathcal{W}^{\prime}}\left|\mathcal{C}\left(\mathcal{D} | \mathcal{W}^{\prime}\right)-\mathcal{C}(\mathcal{D} | \mathcal{W})\right|
```
通过将损失函数C在hi=0出进行Taylor展开
```math
\mathcal{C}\left(\mathcal{D}, h_{i}\right)=\mathcal{C}\left(\mathcal{D}, h_{i}=0\right)+\frac{\delta \mathcal{C}}{\delta h_{i}} h_{i}+R_{1}\left(h_{i}=0\right)
```

因此就可以将损失函数的衰减转化成损失函数对feature map的梯度和feature map激活乘积的绝对值，这样就能够用来评价参数的重要性
```math
\left|\Delta \mathcal{C}\left(h_{i}\right)\right|=\left|\mathcal{C}\left(\mathcal{D}, h_{i}\right)-\frac{\delta \mathcal{C}}{\delta h_{i}} h_{i}-\mathcal{C}\left(\mathcal{D}, h_{i}\right)\right|=\left|\frac{\delta \mathcal{C}}{\delta h_{i}} h_{i}\right|
```

#### LDA-Pruned（CVPR2017）
经过LDA分析发现对于每一个类别，有很多filter之间的激活是高度不相关的，因此可以利用这点来剔除大量的只具有少量信息的filter。VGG-16的conv5_3具有512个filter，将每一个filter的输出值中的最大值定义为该filter的fire score，因此对应于每一张图片就具有一个512维的fire向量，当输入一堆图片时，就可以得到一个N*512的fire矩阵，作者用intra-class correlation来衡量filter的重要性
```math
I C C=\frac{s^{2}(b)}{s^{2}(b)+s^{2}(w)}
```
就是LDA公式，所以接下来就是通过LDA降维来删除对分类提取特征判别不强的filter

#### Random Masks（ICLR2017）
作者认为，既然我无法直观上的判定filter的重要性，那么就采取一种随机裁剪的方式，然后对于每一种随机方式统计模型的性能，来确定局部最优的裁剪方式。 这种随机裁剪方式类似于一个随机mask，假设有M个潜在的可裁剪weight，那么一共就有2^M个随机mask。假设裁剪比例为a，那么每层就会随机选取ML*a个filter，一共随机选取N组组合，然后对于这N组组合，统计裁剪掉它们之后模型的性能，然后选取性能最高的那组作为局部最优的裁剪方式。

#### ThiNet（ICCV2017）
考虑相邻网络层的给出重要性判别。如果可以用某一层的输入的一个子集S代替原来的输入得到尽可能类似原来的输出的话，那么子集以外的输入就可以去掉，同时其对应的前面一层的filter也就可以去掉。本文采用贪心算法来求解最优的集合S，定义压缩率r，找到能使优化式子最小的channel集合S，从而去除冗余的filter。这里贪心法是通过对每一个channel进行依次删除，若删除后准确率不影响，继续下一个channel，若影响，就不删除。