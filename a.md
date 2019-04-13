## 建模与问题解决流程
### 1.数据处理
###    数据预处理(清洗， 调权)

![60d9b999b743dced19264b9612db2339.png](en-resource://database/495:0)
### 2.特征工程
###    特征工程
![71fe6676d4e34f39d4a53997be3acd81.png](en-resource://database/497:0)、

![95fd0f111885e67b20a43e740923e72e.png](en-resource://database/499:0)
### 3.模型选择

#### 模型选择方法
#### 模型参数选择
#### 模型状态评估
#### 交叉验证模型

### 4.寻找最佳超参数： 交叉验证

###   5.模型分析与模型融合
#### 模型融合
##### Bagging
######  Œ  用一个算法

Ø  不用全部的数据集， 每次取一个子集训练一个模型

Ø  分类： 用这些模型的结果做vote

Ø  回归： 对这些模型的结果取平均

######    用不同的算法

Ø  用这些模型的结果做vote 或 求平均

##### Stacking
![3736884d25d945da500fc6ddc72fa82a.png](en-resource://database/501:0)

![4f7a35a719a2a38c19f00783899908c8.png](en-resource://database/503:0)

##### Boosting
![a312b5a257c25cfddc903b8928f66bee.png](en-resource://database/505:0)

## 解决问题流程

 o  了解场景和目标

o  了解评估准则

o  认识数据

 o  数据预处理(清洗， 调权)

o  特征工程

o  模型调参

o  模型状态分析

o  模型融合
