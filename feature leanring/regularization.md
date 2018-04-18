### 4.0 过拟合
过拟合（`overfitting`）是指在模型参数拟合过程中的问题，由于训练数据包含**抽样误差**，训练时，复杂的模型将抽样误差也考虑在内，将抽样误差也进行了很好的拟合。

![过拟合](https://pic4.zhimg.com/v2-62b74afd353d7fdaf9c8d6b20d38d3e1_r.jpg)

针对过拟合问题，通常会考虑以下途径来解决：
a) 减少特征的数量：
- 人工的选择保留哪些特征；
- 模型选择算法（之后的课程会介绍）

b) 正则化
- 保留所有的特征，但是降低参数的量/值；
- 正则化的好处是当特征很多时，每一个特征都会对预测y贡献一份合适的力量；

c) 获取更多的数据
- **从源头获取数据**(但是，在很多情况下，大幅增加数据本身就不容易；另外，我们不清楚获取多少数据才算够；)
- **根据当前数据集估计数据分布参数，使用该分布产生更多数据**：这个一般不用，因为估计分布参数的过程也会代入抽样误差。
- 数据增强(`Data Augmentation`):通过一定规则扩充数据。(可以通过图像平移、水平翻转、缩放、裁剪、变形(扭曲)等手段将数据库成倍扩充；)

![Data Augmentation](https://pic4.zhimg.com/v2-c350674aa4dbee1e375c0d3e68ff0e4d_r.jpg)

d) 训练时间
对于每个神经元而言，其激活函数在不同区间的性能是不同的：

![sigmoid性能](https://pic3.zhimg.com/v2-f3121f5af646c8a5a1e239594557098e_r.jpg)

当网络权值较小时，神经元的激活函数工作在线性区，此时神经元的拟合能力较弱（类似线性神经元）。

有了上述共识之后，我们就可以解释为什么限制训练时间（`early stopping`）有用：因为我们在初始化网络的时候一般都是初始为较小的权值。**训练时间越长，部分网络权值可能越大**。如果我们在合适时间停止训练，就可以将网络的能力限制在一定范围内。

e) 增加噪声

- 在输入中加噪声
- 在权值上加噪声
- 对网络的响应加噪声

f) 结合多种模型
- `Bagging`

简单理解，就是分段函数的概念：用不同的模型拟合不同部分的训练集。

- `Boosting`

既然训练复杂神经网络比较慢，那我们就可以只使用简单的神经网络(层数、神经元数限制等)。通过训练一系列简单的神经网络，加权平均其输出。

![boosting_weight](https://pic1.zhimg.com/v2-a64fbfad58458c6321fa2dd75ed99fcd_r.jpg)

- `dropout`

在训练时，每次随机（如50%概率）忽略隐层的某些节点；这样，我们相当于随机从2^H个模型中采样选择模型；同时，由于每个网络只见过一个训练数据（每次都是随机的新网络），所以类似 `bagging` 的做法。

详细参考: [dropout](https://github.com/le773/PythonDebug/blob/84f39287718277f7dd78e77301bf19e47b99fe4e/deep%20learning/tensorflow%20with%20neural%20network%20introduction.md "dropout")

g) 贝叶斯

![bayes](https://pic3.zhimg.com/v2-88170130d8bac2f6f54998473ec99b95_r.jpg)

h) `Early stopping`

![early_stop_1.png](https://i.imgur.com/ju1QlUX.png)

缺点：不能独立的处理梯度下降和防止过拟合，因为过早的停止梯度下降也就是停止了优化代价函数，导致模型考虑的的东西变得复杂。

优点：运行一次梯度下降，可以找到权重`w`较小值、中间值、较大值等；`L2`正则化则需要结合网络寻找最优`λ`

### 4.1 解决过拟合总结
![overfitting](https://pic2.zhimg.com/v2-1c0588c97d1302b0e7bc8c6d5eede473_r.jpg)

### 5.0 正则化
该算法可以平衡特征的数量、精确度、泛化能力，牺牲一定的准确性，而增加一定的泛化性能，避免完美拟合。

```
from sklearn import linear_model
clf = linear_model.Lasso()
clf.fit(features,labels)
print(clf.coef_)            #输出每个特征所占的比例，为0时说明被舍弃了
```

#### L1正则化和L2正则化的说明

- **L1正则化**是指权值向量w中各个元素的绝对值之和，通常表示为||w||1
- **L2正则化**是指权值向量w中各个元素的平方和然后再求平方根（可以看到Ridge回归的L2正则化项有平方符号），通常表示为||w||2

贝叶斯学派的观点：正则化其实就是对模型的参数设定一个先验。
L1正则是laplace先验，l2是高斯先验，分别由参数sigma确定。

#### 下面是L1正则化和L2正则化的作用

- L1正则化可以产生**稀疏**权值矩阵，即产生一个稀疏模型，可以用于特征选择(删掉一些冗余的特征)
- L2正则化可以防止模型过拟合(`overfitting`)；一定程度上，L1也可以防止过拟合

### 5.1 Lasso回归的损失函数
下图是Python中Lasso回归的损失函数，式中加号后面一项α||w||1即为L1正则化项。

![Lasso.png](https://i.imgur.com/mnBUkTZ.png)

下图是Python中Ridge回归的损失函数，式中加号后面一项![L2Reg](https://i.imgur.com/PhdhMdR.png)即为L2正则化项。

![Ridge.png](https://i.imgur.com/IvfSwSP.png)


#### 5.2.1 L1正则化和特征选择
假设有如下带L1正则化的损失函数： 

![L1_reg_func_1](https://i.imgur.com/DPdbKJv.png)

其中J0是原始的损失函数，加号后面的一项是L1正则化项，α是正则化系数。注意到L1正则化是权值的绝对值之和，J是带有绝对值符号的函数，因此J是不完全可微的。机器学习的任务就是要通过一些方法（比如梯度下降）求出损失函数的最小值。当我们在原始损失函数J0后添加L1正则化项时，相当于对J0做了一个约束。令`L=α∑w|w|`，则`J=J0+L`，此时我们的任务变成在L约束下求出J0取最小值的解。考虑二维的情况，即只有两个权值w1和w2，此时`L=|w1|+|w2|`对于梯度下降法，求解J0的过程可以画出等值线，同时L1正则化的函数L也可以在w1w2的二维平面上画出来。如下图：

![L1Reg_model_1.png](https://i.imgur.com/sHE39w4.png)

图中等值线是J0的等值线，黑色方形是L函数的图形。在图中，当J0等值线与L图形首次相交的地方就是最优解。上图中J0与L在L的一个顶点处相交，这个顶点就是最优解。注意到这个顶点的值是(w1,w2)=(0,w)。可以直观想象，因为L函数有很多『突出的角』（二维情况下四个，多维情况下更多），J0与这些角接触的机率会远大于与L其它部位接触的机率，而在这些角上，会有很多权值等于0，这就是为什么L1正则化可以产生稀疏模型，进而可以用于特征选择。

而正则化前面的系数α，可以控制L图形的大小。α越小，L的图形越大（上图中的黑色方框）；α越大，L的图形就越小，可以小到黑色方框只超出原点范围一点点，这是最优点的值(w1,w2)=(0,w)中的w可以取到很小的值。

类似，假设有如下带L2正则化的损失函数： 

![L1_reg_func_2](https://i.imgur.com/SPrjJvh.png)

同样可以画出他们在二维平面上的图形，如下：

![L2Reg_model_2.png](https://i.imgur.com/LFVWAkg.png)

二维平面下L2正则化的函数图形是个圆，与方形相比，被磨去了棱角。因此J0与L相交时使得w1或w2等于零的机率小了许多，这就是为什么L2正则化不具有稀疏性的原因。

#### 5.2.2 L2正则化和过拟合

![L2_reg_model_2](https://i.imgur.com/RyXIsIW.png)

其中λ就是正则化参数。从上式可以看到，与未添加L2正则化的迭代公式相比，每一次迭代，θj都要先乘以一个小于1的因子，从而使得θj不断减小，因此总得来看，θ是不断减小的。

λ越大，θj衰减得越快

[机器学习中正则化项L1和L2的直观理解](https://blog.csdn.net/jinping_shi/article/details/52433975)

#### 5.2.3 上述公式5的推导数过程
- 在公式3添加L2正则化

![gd_costfunction_4.jpg](https://i.imgur.com/gGLaAZe.jpg)

- 对theta求导数

![gd_costfunction_6.jpg](https://i.imgur.com/eGyAJng.jpg)

- 梯度下降

![gd_costfunction_7.jpg](https://i.imgur.com/i1o7bCw.jpg)

- 没有正则化时 theta的权重为1，现在

![gd_costfunction_8.jpg](https://i.imgur.com/VIDSOQu.jpg)

即权重衰减

#### 5.3 L2 正则化
![gd_costfunction_9.jpg](https://i.imgur.com/QFrKjrL.jpg)

![gd_costfunction_10.jpg](https://i.imgur.com/fx5wLTv.jpg)

对参数添加一个系数，使施加的影响最小。

参考
[关于L2范数如何避免过拟合？](https://www.zhihu.com/question/30231749 "关于L2范数如何避免过拟合？")


#### 5.4 Logistic regresession 正则化

![logistic_regression_regulation_1.png](https://i.imgur.com/WrLCBxc.png)

`λ`是正则化参数，通常通过交叉验证，寻找最好的参数。

##### 5.4.1 为什么只正则化参数w, 而不加上参数b ?
因为`w`通常是一个高维参数矢量(几乎涵盖所有参数)，已经可以表达高偏差问题。

`w`可能包含很多参数，但我们不可能拟合所有参数。

`b`只是单个数字，如果加上`b`，也没有什么影响，因为`b`只是众多参数中的一个；通常忽略不计。


#### 5.5 Neural network 正则化
`L2`正则化也称为权重衰减。

![neural_network_regulation_1.png](https://i.imgur.com/7jK8wLo.png)

### 6.0 为什么正则化可以减少过拟合 ?
![neural_network_regulation_2.png](https://i.imgur.com/HqapLjS.png)

直观的理解，`λ`被设置越大，权重矩阵`w`被设置位接近于0的值，也就是把多隐藏单元的权重设为0，也就大大简化了神经网络会变成一个很小的网络，小到如同一个逻辑回归单元，可是深度却很大，它会使这个网络从过拟合的状态更接近于左图的高偏差状态，调整`λ`就可以变成中图的情况。

实际情况是，该神经网络的所有隐藏单元依然存在，但是它们的影响变小了，神经网络变简单，更不容易发生过拟合。

![neural_network_regulation_3.png](https://i.imgur.com/eo59JbK.png)

正则化参数`λ`被设置越大，`w`就越小，`b`忽略不计，`z`也就越小，激活函数越近似线性函数，那么整个神经网络会计算线性函数近的值，整个模型就比较简单，不会发生过拟合。

### 7.0 其它正则化方法