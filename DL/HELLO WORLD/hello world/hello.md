[TOC]
# hello world of DL
## Handwriting Digit Recognition
### MNIST数据集
data 少
### the process of DL

*  **define a set of function**
1.Input & Output
2.choose right Activation Function

*  **goodness of function**
1.choose Proper Loss Function

* **pick the best functon**
1.Gradient Descent

* [ ] ForwardPropagation + BackPropagation compute Gradient
* [ ] update parametric
* [ ] mini-batch

2. 改进梯度下降算法
Adaptive Learning Rate

### keras
#### 操作大概
**define a set of function:**
`model=Sequential( )` #
```
model.add( Dense(input dim =28*28,output dim=500)
model.add(Activation('sigmoid'))
model.add( Dense(output dim=500))
model.add(Activation('sigmoid'))
model.add( Dense(output _dim=10))
model.add(Activation('softmax'))

```
![](https://github.com/JasCoops/NOTES/blob/master/DL/HELLO%20WORLD/hello%20world/%E6%8D%95%E8%8E%B7.PNG?raw=true)


**goodness of function**
<u>*Training Data & Loss Function*</u>
#### proper loss function
```
model.comple(loss='categorical,crossentropy',optimizer='adam',metrics=['accuracy'])
```
![d67a8fd68c536f57058044202f1fe8ac.png](en-resource://database/553:1)

**pick the best functon**
#### Mini batch
* configuration

```
model.compile( loss= 'categorical _ crossentropy ' , optimizer = 'adam' , metrics = [ 'accuracy'] )
```

* find the optimal network paramenters
`
```
model . fit ( x_train , y_train , batch_size =100 ,nb_epoch=20)
```
x_train : image ; y_train : labels
![4137346f7bbb72b251b57ce5a8166ffb.png](en-resource://database/555:1)

输入张量，输出矩阵
![4a5023a4c101458d304f35dd7dd3239d.png](en-resource://database/557:1)
 
**普通下降**

**批量操作** *<u>mini-batch*</u>
类似与批量梯度下降，比较稳定

* batch_size

* epoch

![586ed6a6ec635a83309772c01dda4dc8.png](en-resource://database/563:1)

**随机下降** <u>*Stochastic gradient descent*</u>

* 速度快

实际操作
![7c9f020a308ac1563749b5163a7bd3dd.png](en-resource://database/567:1)
为什么更快？GPU并行运算
为什么更倾向于随机下降？更稳定
能不能那把size开的更大点？
very large batch size can yield(产生) worse performance
#### 实现代码
**归一化**
**batch size**
**loss function**
**optimizer**
**aviation function**

#### keras操作中容易遇到的问题
1.神经网络层数的选择
2.神经网络每层单元数的选择

#### 注意点
1.一定要 test 和 evaluate
因为有可能出现56-layer还没20-layer表现的好


## How to get the best function?
![0b681ef50950a8a98bbb8cd8eda27919.png](en-resource://database/573:1)

### get good results on training data.


#### new activation function
##### sigmoid函数
问题：vanishing gradient problem
1.当layer过多的时候，前面的几层还在迭代的时候，最后几层已经converge了，当layer过多的时候，输出local min
2.当layer过多的时候，前几层的参数拥有smaller gradients，对迭代的作用不明显，对cost和output影响很小

##### RELU
相当于无数sigmoid叠加，解决梯度消失问题

![e82fd7589881f5497af8aef93b4fa206.png](en-resource://database/575:1)

z<=0 , a=0 , 减少一些input的影响，增加运算速度
z>0 , a=z linear ，但整体还是non-linear的

###### 改进
![2e11a73a8b72ff727dce256efe86ca68.png](en-resource://database/581:1)

##### Maxout
相当于CNN的MAX池化，也就没有激活函数了
要调的参数：group的meber数量（2，3，4，5

可包含ReLU
它是一个**Learnable Activation Function **
![2162302fb6bdbb5881bf6d26d7e191a4.png](en-resource://database/585:1)

取决于w和b还有group的member数
**can be any piecewise linear convex function**

![9d40b1b135d41eae3c557b8be939f50e.png](en-resource://database/587:1)

#### Adaptive learning rate
dynamic 的变换LR
##### Adagrad
![468bfe56e2b873c1d18ae66fdecb4256.png](en-resource://database/589:1)
w（t+1）:=w（t）-固定lr/过去所有梯度平方和再开根号 * 现在的梯度值g（t) 以更新参数

##### RMSProp
![6167df30639b79656981d8d320838763.png](en-resource://database/591:1)

α 小，则倾向于相信新的gradient

![456a7e4379f1a77b340ec42f7f4cdbea.png](en-resource://database/593:1)
神经网络训练不好的结果

* 卡在local minima
* 卡在saddle point  鞍点
* very slow at the plateau 再坡度小的地方迭代较慢

#### Momentum

传统的Gradient Descent :
![26b7fcab88ef1990acc197f758509a88.png](en-resource://database/597:1)

Momentum
![4bca59d74ab5d911728a3030a999e0cc.png](en-resource://database/599:1)

##### Adam

![ae24a8cdbdce471e5349c81617706bef.png](en-resource://database/601:1)

#### Proper Loss Function
##### 均方差损失函数（MSE）

![1abe1b98285be5f5c4fe6f9cbd0360c8.png](en-resource://database/607:1)

##### binary_crossentropy（交叉熵损失函数）
一般用于**二分**类：
![8d4279f78970567fd69f65c08d143816.png](en-resource://database/605:1)

##### categorical_crossentropy loss（分类交叉熵损失函数）
一般用于**多分**类：

n是样本数，m是分类数，注意，这是一个多输出的loss的函数
![ec0e69df4a26c28dec7d0272442738ec.png](en-resource://database/603:1)

### get good results on testing data.
#### Early Stopping(for good results on testing data)
这里的testing set指的是有label的testing set。
如果learning rate设得对的话，training set的loss会逐渐降低，而testing set与training set可能分布不同，所以testing set的loss可能先降后升，这时就不要一直train下去，而是要在testing loss最小的地方停止train。这里的testing set 实际指的是validation set。 
#### Regularization
##### L2正则化
![9dce15eeef0dd371bba26d70accc00c1.png](en-resource://database/609:1)

L2正则化让function更平滑，而bias与函数平滑程度没有关系。
参数更新：
![f4baaf261f9c8cd160e289340784a40d.png](en-resource://database/611:1)

正则化在NN中虽有用但不明显。
NN参数初始值一般接近0，update参数即是要参数原理0。L2正则化（让参数接近0）的作用可能与early stopping类似。
##### L1正则化
![496ba3519bfe6d526df9372b40a65d3f.png](en-resource://database/613:1)

#### dropout方法
![e0ebe6c358a1a463f88b5a0630c4603f.png](en-resource://database/571:1)
在test结果不好的时候，才apply的
有时候你train结果都不好，就冒用dropout，会越test越train越差的
##### 出现背景
在训练神经网络的时候经常会遇到过拟合的问题，过拟合具体表现在：模型在训练数据上损失函数较小，预测准确率较高；但是在测试数据上损失函数比较大，预测准确率较低。

如果模型过拟合，那么得到的模型几乎不能用。为了解决过拟合问题，一般会采用模型集成的方法，即训练多个模型进行组合。此时，训练模型费时就成为一个很大的问题，不仅训练多个模型费时，测试多个模型也是很费时。

训练深度神经网络的时候，总是会遇到两大缺点：
（1）容易过拟合
（2）费时

Dropout可以比较有效的缓解过拟合的发生，在一定程度上达到正则化的效果。

##### 原理
Dropout可以作为训练深度神经网络的一种trick供选择。在每个训练批次中，通过忽略一半的特征检测器（让一半的隐层节点值为0），可以明显地减少过拟合现象。这种方式可以减少特征检测器（隐层节点）间的相互作用，检测器相互作用是指某些检测器依赖其他检测器才能发挥作用。

Dropout说的简单一点就是：我们在前向传播的时候，让某个神经元的激活值以一定的概率p停止工作，这样可以使模型泛化性更强，因为它不会太依赖某些局部的特征。

![310d6da4f55c3d869e762a9698522cf8.png](en-resource://database/569:1)
