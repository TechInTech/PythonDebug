﻿### 01 Standard Large-Margin Problem
![standard_large-Margin_1.png](https://i.imgur.com/W4XaVnO.png)

因为点`x'`和`x''`在超平面![超平面公式](http://img.blog.csdn.net/20131107201104906)上，则有：
1. w<sup>T</sup> x' + b = 0       (1)
2. w<sup>T</sup> x'' + b = 0      (2)

`w`是平面 w<sup>T</sup>的垂直向量，由 (2) - (1) 得:
<center>w<sup>T</sup>(x'' - x') = 0</center>
那么，向量(x'' - x')于平面w<sup>T</sup>上；接下来计算向量(x - x')在向量w上的投影长度:

![standard_large-Margin_2.png](https://i.imgur.com/8cnTPld.png)

假设，超平面能将所有训练样本分类，那么：

![standard_large-Margin_3.png](https://i.imgur.com/q1UL4cn.png)

将上述公式，简写为一个公式，这个公式表示为函数间隔：

![standard_large-Margin_4.png](https://i.imgur.com/z2yGJkf.png)

所有训练样本到超平面的几何距离表示为：

![standard_large-Margin_5.png](https://i.imgur.com/5lxMsrD.png)

考虑支持向量到平面的距离，即是支持向量`w<sup>T</sup> x + b = 1`到超平面的距离，推导如下：

![standard_large-Margin_6.png](https://i.imgur.com/usQlyUf.png)

求max(1/||w||)，可以等价于标准问题：min (0.5 * w * w<sup>T</sup>)

![standard_large-Margin_8.png](https://i.imgur.com/MeDSMnh.png)

下图的含义是，在训练样本中，样本到超平面最小的距离是1：

![standard_large-Margin_9.png](https://i.imgur.com/B1pR82z.png)

`support vector`：是寻找最佳超平面的样本，其它的样本对寻找最佳超平面是没有作用的。

![standard_large-Margin_10.png](https://i.imgur.com/KOwcg6v.png)

在下图中，虚线经过的点就是`support vector`

![standard_large-Margin_11.jpg](https://i.imgur.com/lMlaZ1g.jpg)


----------

### 02  Solving General SVM

#### 02.01 转化为凸二次规划

最大化`1/(w.T)`转化为约束最优化问题：

![凸二次规划](http://ww4.sinaimg.cn/large/6cbb8645gw1ewo7sn30ngj208m02ct8l.jpg)

平方项保证了表达式的单调性，它会放大结果但不会改变表达式的顺序。

----------

### 03 Why Large-Margin Hyperplane
`regularization`:测量误差最小，且满足ww<sup>T</sup> < C

`SVM`：最小化ww<sup>T</sup>，且满足训练样本无错分。

`SVM`和`regularization`目标和限制条件分别对调，其实，考虑的内容是类似的，效果也是相近的。`SVM`也可以说是一种`weight-decay` `regularization`且测量误差为0

![standard_large-Margin_12.png](https://i.imgur.com/a2Kcpcg.png)


### 04 Large-Margin Restricts Dichotomies
![standard_large-Margin_13.png](https://i.imgur.com/UpPnV7h.png)

不看虑软间隔，满足最小间隔距离的的分割面可能不存在。

### 05 Lagrange Function
首先定义原始目标函数`f(x)`，拉格朗日乘子法的基本思想是把约束条件转化为新的目标函数`L(x,α)`的一部分，从而使有约束优化问题变成我们习惯的无约束优化问题。

![Larange_f_1.png](https://i.imgur.com/FqAVMDI.png)

α<sub>n</sub>是第`n`个训练样本的拉格朗日乘子。

上述的添加拉格朗日乘子后的不等式是合页损失函数(hinge loss)。

![hinge_loss_1.png](https://i.imgur.com/CR1Mcqy.png)

上图虚线显示的是感知机的损失函数[y<sub>i</sub>(w\*x<sub>i</sub> + b)]。当样本点(x<sub>i</sub>,y<sub>i</sub>)被正确分类时，损失是0，否则损失是[-y<sub>i</sub>(w\*x<sub>i</sub> + b)]。

相比之下，合页损失函数不仅要分类正确，而且确信度足够高时损失才是0。也就是说，合页损失函数对学习有更高的要求。

----------

#### 05.01 最小问题包含最大问题
![Larange_f_2.png](https://i.imgur.com/uc7mcv4.png)

定义函数θ<sub>p</sub>(w,b)：

![svm_lagelangri_14.png](https://i.imgur.com/DoC2Awy.png)

如果`b w`不满足约束条件，则1 - y<sub>n</sub>(w<sup>T</sup> * z<sub>n</sub> + b ) > 0，如果要使使拉格朗日函数最大，则需要α更大，显然此时无法求得最小的SVM；

反之`b w`满足约束条件，那么当`α=0`时，`svm`得到最小值。

所以有，在`b w`满足原始问题约束的条件下，θ<sub>p</sub>(x)=0.5 \* w<sup>T</sup> \* w

把原始问题中的s.t.条件去掉，得到原始问题的等价问题：

![svm_lagelangri_15.png](https://i.imgur.com/WDf2Ewx.png)

----------

### 06 Lagrange Dual Problem

![Larange_f_3.png](https://i.imgur.com/7zVveOh.png)

不等式右侧，固定α'<sub>n</sub>且α'<sub>n</sub>>=0，改变`b w`取最小值，此时求得最小值时有`b1 w1`

那么对于不等式左侧，相当于固定`b1 w1`，更改α'<sub>n</sub>求得最大值，显然上述不等式成立。

那么，对于所有的α'<sub>n</sub>≥0，取最大化：

![Larange_f_4.png](https://i.imgur.com/ji6BB8L.png)

上述不等式，右侧是svm问题的下界.

右侧：固定`α'`调整`b2 w2`，求最小拉格朗日函数中的最大值

左侧：固定右侧得到的`b2 w2`调整`α`，求最大拉格朗日函数中的最小值

显然，对于不等式成立；上述不等式两边可以看到 min和max交换，所以称为拉格朗日对偶问题。

转化为对偶问题的优势：无约束条件

证明：

![Larange_f_5.png](https://www.zhihu.com/equation?tex=%5Ctheta_D%28%5Cboldsymbol%7B%5Calpha%7D%2C%5Cboldsymbol%7B%5Cbeta%7D%29%3D%5Cmin_%7B%5Cboldsymbol%7Bx%7D%7DL%28%5Cboldsymbol%7Bx%7D%2C%5Cboldsymbol%7B%5Calpha%7D%2C%5Cboldsymbol%7B%5Cbeta%7D%29+%5Cleq+L%28%5Cboldsymbol%7Bx%7D%2C%5Cboldsymbol%7B%5Calpha%7D%2C%5Cboldsymbol%7B%5Cbeta%7D%29+%5Cleq+%5Cmax_%7B%5Cboldsymbol%7B%5Calpha%7D%2C%7E%5Cboldsymbol%7B%5Cbeta%7D%3B%7E%5Cbeta_j%5Cgeq0%7DL%28%5Cboldsymbol%7Bx%7D%2C%5Cboldsymbol%7B%5Calpha%7D%2C%5Cboldsymbol%7B%5Cbeta%7D%29+%3D+%5Ctheta_P%28%5Cboldsymbol%7Bx%7D%29)

已知≥是一种弱对偶关系，在二次规划`QP`问题中，如果满足以下三个条件：

![Larange_f_6.png](https://i.imgur.com/PfIpdvM.png)

那么，上述不等式关系就变成强对偶关系，`≥`变成`=`，即一定存在满足条件的解`(b,w,α)`，使等式左边和右边都成立，`SVM`的解就转化为右边的形式。

### 07 Solving Larange Dual:Simplifications
转化为对偶问题后，max min(...)中min(...)无等式无约束条件，有利于求解，等式展开后：

![Larange_f_7.png](https://i.imgur.com/kVUmrCt.png)

最小值是在谷底，即梯度为0的点，梯度为0(导数为0)，则有对`b`求导，令`L`对参数`b`的梯度为零：

![Larange_f_8.png](https://i.imgur.com/sMXMzVQ.png)

求得sum(α<sub>n</sub>y<sub>n</sub>)=0，那么简化代价函数

![Larange_f_9.png](https://i.imgur.com/z7cOjT0.png)

去除`b`后的等式

![Larange_f_10.png](https://i.imgur.com/45KPruR.png)

对`w`求导，令`L`对参数`w`的梯度为零：

![Larange_f_11.png](https://i.imgur.com/LCj5H1s.png)

得到：

![Larange_f_14.png](https://i.imgur.com/NsrBR8O.png)

然后，将`w`带入上式：

![Larange_f_12.png](https://i.imgur.com/4nQfnOv.png)

拉格朗日对偶问题的简化版

![Larange_f_13.png](https://i.imgur.com/1rXuBc5.png)


### 08 Karush-Kuhn-Tucker conditions

![Larange_f_16.png](https://i.imgur.com/Ar3TCI3.png)

### 09 Dual Formulation of Support Vector Machine
#### 09.01 Dual Formulation of Support Vector Machine
将`max`问题转化为`min`问题:

![Larange_f_19.png](https://i.imgur.com/pdk10do.png)

<!-- 令![lagelangri_1.jpg](https://i.imgur.com/v4sIqYG.jpg) -->

<!-- 当某个约束条件不满足时，例如y<sub>i</sub>(w<sup>T</sup>x<sub>i</sub> + b)<1，那么显然有θ(w)=∞(只要令α<sub>i</sub>=∞即可)。而当所有条件都满足时，则最优值为θ(w)= 0.5 x |w| x |w|，即最初要最小化的量。-->

<!-- 因此，在要求约束条件得到满足的情况下最小化 0.5 x |w| x |w|，实际上等价于直接最小化θ(w)(当然，这里也有条件约束，就是α<sub>i</sub>)，因为如果约束条件没有得到满足，θ(w)就会等于无穷大，自然不是我们要求的最小值。-->

<!-- 具体写出来，目标函数变成了：-->

<!-- ![lagelangri_2.jpg](https://i.imgur.com/Ygl4qLC.jpg)-->

<!-- 这里用p<sup>*</sup>表示这个问题的最优价，且和最初的问题是等价的。如果直接求解，那么一上来便是面对w和b两个参数，而α<sub>i</sub>又是不等式约束，这个求解过程不好做，于是：-->

<!-- ![lagelangri_3.jpg](https://i.imgur.com/uT7uuK1.jpg)-->

<!-- 交换以后的新问题是原始问题的对偶问题，这个新问题的最优值用d<sup>*</sup>来表示，在满足某些条件的情况下，这两者相等，这个时候就可以通过求解对偶问题来间接的求解原始问题。-->
#### 09.02 目标函数转换的证明
定理1：对于任意α,β和x有：

![lagelangri_4.png](https://i.imgur.com/NMb7MZX.png)

证明：

![lagelangri_5.png](https://i.imgur.com/QMegMUI.png)

即

![lagelangri_6.png](https://i.imgur.com/HCW6VlZ.png)

所以

![lagelangri_7.png](https://i.imgur.com/9yuPkCy.png)

即：d<sup>\*</sup> < q<sup>\*</sup>

d<sup>\*</sup>、q<sup>\*</sup>分别是对偶问题和原始问题的最优值。

#### 09.03 定理1的推论
如果能够找到一组x<sup>\*</sup>，α<sup>\*</sup>、β<sup>\*</sup>，使得θ<sub>D</sub>(α<sup>\*</sup>,β<sup>\*</sup>)=θ<sub>P</sub>(x<sup>\*</sup>)，那么就应该有

θ<sub>D</sub>(α<sup>\*</sup>,β<sup>\*</sup>) = d<sup>\*</sup>

θ<sub>P</sub>(x<sup>\*</sup>) = q<sup>\*</sup>

d<sup>\*</sup> = q<sup>\*</sup>

当d<sup>\*</sup> < q<sup>\*</sup>时，称原始问题与对偶问题之间“弱对偶性”成立；

当d<sup>\*</sup> = q<sup>\*</sup>时，则“强对偶性”成立；


#### 09.04 对偶问题求解 第1步

根据对`w`，`b`求导，得到`w`，`b`的值，代入上述公式

![Larange_f_21.png](https://i.imgur.com/xQD5Qyb.png)

根据多项式乘法的基本规律（所有项和的积等于所有项积的和）

![Larange_f_22.png](https://i.imgur.com/9ty4ytV.png)

代入公式可得：

![Larange_f_20.png](https://i.imgur.com/TE6FCdw.png)

#### 09.05 上述结论的详细推导公式
![lagelangri_8.png](https://i.imgur.com/OU9AIQu.png)

其中b=0，优化公式后即为 09.04 对偶问题求解 第1步 给出的结论。

#### 09.06 对偶问题求解 第2步
求对α的极大，即是关于对偶问题的最优化问题。经过上面的求w、b，得到拉格朗日式子已经没有变量w、b，只有α。从上面的式子得到：

![lagelangri_9.png](https://i.imgur.com/mHMQP39.jpg)

### 10 Dual SVM with QP Solver
#### 10.01 Dual SVM with QP Solver
![Larange_f_18.png](https://i.imgur.com/a7UrTjC.png)

求`α`的值

![Larange_f_23.png](https://i.imgur.com/pDa7J3d.png)

根据`α`求`w`，`b`

![Larange_f_24.png](https://i.imgur.com/rDVHw24.png)

----------
#### 10.02 此时α已经通过凸二次优化解出

定理：设α<sup>\*</sup>=(α<sub>1</sub><sup>\*</sup>,α<sub>2</sub><sup>\*</sup>,...,α<sub>N</sub><sup>\*</sup>)<sup>T</sup>是对偶问题的(09.06)一个解。若存在α<sup>\*</sup>的一个分量α<sub>j</sub><sup>\*</sup>，0< α<sub>j</sub><sup>\*</sup> < C，则原始问题(03)的解可按下式求得：

![lagelangri_10.png](https://i.imgur.com/COrpg3G.png)

若存在α<sup>\*</sup>的一个分量α<sub>j</sub><sup>\*</sup>，0< α<sub>j</sub><sup>\*</sup> < C，则 [y<sub>i</sub>(w<sup>\*</sup>x<sub>i</sub> + b<sup>\*</sup>) - 1 = 0]

由此定理可知，分离超平面可写成：

![lagelangri_11.png](https://i.imgur.com/yJXpwMW.png)

----------

### 11 核函数
现实任务中，原始样本空间内也许并不存在一个能正确划分两类样本的超平面；对这样的问题，可将样本映射到更高维的特征空间，使得样本在这个特征空间内线性可分。

令`φ(x)`表示将`x`映射后的特征向量，也是在特征空间中划分超平面所对应的模型为：

![svm_kernel_2.png](https://i.imgur.com/h1PSsYr.png)

转化为最优化问题

![svm_kernel_3.png](https://i.imgur.com/HUV8u3c.png)

其对偶问题是

![svm_kernel_4.png](https://i.imgur.com/Lndal2a.png)

![svm_kernel_5.png](https://i.imgur.com/cYbOABq.png)

分类决策函数式成为：

![lagelangri_12.png](https://i.imgur.com/Sy8WYyP.png)

常用核函数

![svm_kernel_1.png](https://i.imgur.com/eMLCvZP.png)

#### 11.01 Linear Kernel
`Linear Kernel：K(x, x') = xTx'`

- 优点
`safe`（一般不太会`overfitting`，所以线性的永远是我们的首选方案）；
`fast`，可以直接使用`General SVM`的`QP`方法来求解，比较迅速；
`explainable`，可解释性较好，我们可以直接得到`w, b`，它们直接对应每个`feature`的权重。

- 缺点
restrict：如果是线性不可分的资料就不太适用了！

#### 11.02 Polynomial Kernel
`Polynomial Kernel: K(x, x') = (ζ + γxTx')Q`

- 优点
我们可以通过控制`Q`的大小任意改变模型的复杂度，一定程度上解决线性不可分的问题；

- 缺点
含有三个参数，太多啦！

#### 11.03 径向基核
径向基函数是一个采用向量作为自变量的函数，能够基于向量距离运算输出一个标量。

![径向基核](http://img.my.csdn.net/uploads/201304/03/1364958259_8460.jpg)

其中，σ是用户定义的用于确定到达率或者说函数值跌落到0的速度参数。

注：使用径向基核前，应对`feature`进行归一化
#### 11.03.01 参数分析
- `γ`参数实际上对 `SVM` 的“线性”核函数没有影响。核函数的重要参数是`C`, 
- `C`参数
1. `C`越大，相当于惩罚松弛变量，希望松弛变量接近0，即对误分类的惩罚增大，趋向于对训练集全分对的情况，这样对训练集测试时准确率很高，但泛化能力弱(过拟合)。 
2. `C`值小，对误分类的惩罚减小，允许容错，将他们当成噪声点，泛化能力较强(容易欠拟合);

- `degree`:多项式`poly`函数的维度;
- `kernel` ：核函数，默认是`rbf`，可以是`linear`, `poly`, `rbf`, `sigmoid`, `precomputed`

#### 11.03.02 RBF公式里面的sigma和gamma的关系

![rbf中的gamma](http://img.blog.csdn.net/20150606105930104?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbHVqaWFuZG9uZzE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

`gamma`是你选择径向基函数作为`kernel`后，该函数自带的一个参数。隐含地决定了数据**映射到新的特征空间后的分布**。

如果`gamma`设的太大，`σ`会很小，`σ`很小的高斯分布长得又高又瘦，会造成只会作用于支持向量样本附近，对于未知样本分类效果很差，存在训练准确率可以很高，(如果让`σ`无穷小，则理论上，高斯核的`SVM`可以拟合任何非线性数据，但容易过拟合)而测试准确率不高的可能，就是通常说的过训练；

而如果设的过小，则会造成平滑效应太大，无法在训练集上得到特别高的准确率，也会影响测试集的准确率。

#### 11.03.03 rbf的优势
建议首选`RBF`核函数进行高维投影，因为：

1. 能够实现非线性映射；（ 线性核函数可以证明是他的一个特例；`SIGMOID`核函数在某些参数上近似RBF的功能。）
2. 参数的数量影响模型的复杂程度，多项式核函数参数较多。
3. `the RBF kernel has less numerical difficulties.`

#### 11.03.04 总结
所以在实际应用中，一般是先使用线性的`kernel`，如果效果不好再使用`gaussian kernel`（小的`γ`）和多项式`kernel`(小的`Q`)。

[svm详解](https://www.cnblogs.com/little-YTMM/p/5547642.html "svm详解")

----------


### 12 软间隔
#### 12.01 软间隔
现实任务中往往很难确定合适的核函数使得训练样本在特征空间中线性可分；即使恰好找到某个核函数使用训练集在特征空间中线性可分，也很难断定这个线性可分结果不是由于过拟合所造成。

缓解该问题的一个办法是允许支持向量机在一些样本上出错，为此，要引入软间隔的概念。

![svm_soft_margin_1.png](https://i.imgur.com/KFMTKhf.png)

在最大化间隔的同时，不满足约束的样本应尽可能少，于是，优化目标可以写为：

![svm_soft_margin_2.png](https://i.imgur.com/KCRyysx.png)

其中`C>0`是一个常数，损失函数的定义：

![svm_soft_margin_3.png](https://i.imgur.com/ruj8EvN.png)

如果采用`hinge`损失，优化目标可以写为：

![svm_soft_margin_4.png](https://i.imgur.com/ItMeXlK.png)

引入松弛变量，优化目标可以写为：

![svm_soft_margin_5.png](https://i.imgur.com/YUKRiTI.png)

![svm_soft_margin_6.png](https://i.imgur.com/IblvhPi.png)

引入松弛变量后的拉格朗日函数：

![svm_soft_margin_7.png](https://i.imgur.com/CHdUTOy.png)

令`L`对`w` `b` `ξ`求偏导数

![svm_soft_margin_8.png](https://i.imgur.com/XUQLemf.png)

对偶问题

![svm_soft_margin_9.png](https://i.imgur.com/525yyVN.png)

软间隔支持向量机，KKT条件要求：

![lagelangri_13.png](https://i.imgur.com/DUnlAL4.png)

#### 12.02 常用替代损失函数
![svm_replace_f_1.png](https://i.imgur.com/gdV8914.png)

![svm_replace_f_2.png](https://i.imgur.com/IpWWx3J.png)

----------

### 13 补充

支持向量与间隔的定义
![standard_large-Margin_7.png](https://i.imgur.com/wyTnBn8.png)

#### 13.01 SVM决策边界
![svm_decision_boundary_1.png](https://i.imgur.com/C8kiPw8.png)

上图，左侧支持向量在超平面切线上投影的距离小于右侧，那么`θl > θr`，所以超平面选择右侧。

----------

#### 13.02 SVM多分类
![svm_muti_classification_1.png](https://i.imgur.com/im9dRcz.png)

和逻辑回归类似，训练`K`个`SVM`，针对每一个分类器训练得到一个`θ`，然后选择对此样本最好的那个参数。

----------

#### 13.03 SVM LogisticRegression
![svm_vs_logisticregression_1.png](https://i.imgur.com/kI0Qnj9.png)

上图中，n是feature的数量 m是样本数

1.如果n相对于m来说很大，则使用LR算法或者不带核函数的SVM（线性分类）n远大于m，n=10000，m=10-1000

理由：特征数相对于训练样本数已经够大了，样本在高维空间里会比较稀疏，使用线性模型就能取得不错的效果，不需要过于复杂的模型；

2.如果n很小，m的数量适中（n=1-1000，m=10-10000）使用带有核函数的SVM算法

理由：在训练样本数量足够大而特征数较小的情况下，可以通过使用复杂核函数的SVM来获得更好的预测性能，而且因为训练样本数量并没有达到百万级，使用复杂核函数的SVM也不会导致运算过慢；

3.如果n很小，m很大（n=1-1000，m=50000+）增加更多的feature然后使用LR算法或者不带核函数的SVM

理由：因为训练样本数量特别大，使用复杂核函数的SVM会导致运算很慢，因此应该考虑通过引入更多特征，然后使用线性核函数的SVM或者lr来构建预测性更好的模型。

4.良好的神经网络模型通常会得到较好的分类，但是训练会比较慢

LR和不带核函数的SVM比较类似。

#### 13.04 扩展：SVM LogisticRegression
1. 特征比数据量还大时，选择什么样的分类器？</br>
线性分类器，因为维度高的时候，数据一般在维度空间里面会比较稀疏，很有可能线性可分。

2. 对于维度极低的特征，你是选择线性还是非线性分类器？</br>
非线性分类器，因为低维空间可能很多特征都跑到一起了，导致线性不可分

线性分类器：</br>
LR,贝叶斯分类，单层感知机、线性回归

非线性分类器：</br>
决策树、RF、GBDT、多层感知机

SVM要看是线性核还是非线性核。
----------

#### 14.01 等式约束
假设有自变量`x`和`y`，给定约束条件`g(x,y)=c`，要求`f(x,y)`在约束`g`下的极值；

![standard_eq_1.jpg](https://i.imgur.com/XRJbQ61.jpg)

#### 14.02 KKT
![kkt_1.png](https://i.imgur.com/NDXvOVd.png)

1. 拉格朗日乘子>=0
2. 约束条件切线的正交线，它们的向量和为0
3. 在最优解处，拉格朗日乘子和约束条件数值和为0

![约束条件下，最优值](https://pic2.zhimg.com/v2-7d8461db6ca62803145bc716851bcca3_r.jpg)

### 15.0 Q&A
#### 15.1 怎么样理解SVM中的hinge-loss？
1.  实现了软间隔分类（这个Loss函数都可以做到）
2.  保持了支持向量机解的稀疏性换用其他的Loss函数的话，SVM就不再是SVM了。

正是因为HingeLoss的零区域对应的正是非支持向量的普通样本，从而所有的普通样本都不参与最终超平面的决定，这才是支持向量机最大的优势所在，对训练样本数目的依赖大大减少，而且提高了训练效率。

#### 15.2 能否对代价函数使用其他的替代损失函数？
如果使用对数损失函数来替代合页损失函数，则几乎得到了log回归模型。实际上，支持向量机与log回归的优化目标接近，通常情况下他们的性能也相当。

log回归优势主要在于其输出具有自然的概率意义，即在给出预测标记的同时也给出了概率。支持向量机的输出不具有概率意义，欲得到概率输出需进行特殊处理。

此外，log回归能直接用于多分类任务，支持向量机为此则需要进行推广。

另一方面，hinge损失有一块“平坦”的零区域，这使得支持向量机的解具有稀疏性，而log损失是光滑的单调递减函数，因此log回归的解依赖于更多的训练样本，其预测开销更大。

#### 15.3 SVM为什么不容易过拟合呢？
1. 自带L2正则项(见：05 Lagrange Function)
L2正则项就能代表模型的复杂度，根据奥卡姆，如果同样效果那么越简单的模型泛化效果越好。所以最优化过程中尽量追求小的L2的值就会提高泛化能力，也就抑制了过拟合的问题。

2. 其次，会通过松弛变量的方法处理掉噪音。
事物都有两面性，对异常点太容忍会导致任意超平面都可以是“最优”超平面，SVM就失去意义了。因此SVM公示中的目标函数也需要相应修改，加上松弛变量的平方和，并求最小值。这样就达到一个平衡：既希望松弛变量存在以解决异常点问题，又不希望松弛变量太大导致分类解决太差。

#### 15.4 支持向量机(SVM)是否适合大规模数据？
1. 支持向量机之所以成为目前最常用，效果最好的分类器之一，在于其优秀的泛化能力，这是是因为其本身的优化目标是结构化风险最小，而不是经验风险最小，因此，通过margin的概念，得到对数据分布的结构化描述，因此减低了对数据规模和数据分布的要求。

2. SVM是非线性方法，a.在样本量比较少的时候，容易抓住数据和特征之间的非线性关系（相比线性分类方法如logistic regression，或者linear SVM）。但是，在样本量比较多的时候，线性分类方法的劣势就要小了很多。b.计算复杂度高。主流的算法是O(n^2)。其中rbf的γ和惩罚项C无法通过概率方法进行计算，只能通过穷举试验来求出。

#### 15.5 如何选择核函数？
使用libsvm，默认参数，RBF核比Linear核效果稍差。通过进行大量参数(C和γ)的尝试，一般能找到比linear核更好的效果。

1. 如果特征维数很高，往往线性可分（SVM解决非线性分类问题的思路就是将样本映射到更高维的特征空间中），可以采用LR或者线性核的SVM；

2. 如果样本数量很多，由于求解最优化问题的时候，目标函数涉及两两样本计算内积，使用高斯核明显计算量会大于线性核，所以手动添加一些特征，使得线性可分，然后可以用LR或者线性核的SVM；

3. 如果不满足上述两点，即特征维数少，样本数量正常，可以使用高斯核的SVM。

#### 15.6 为什么SVM训练的时候耗内存，而预测的时候占内存少？
因为SVM训练过程中需要存储核矩阵。而预测的时候只需要存储支持向量和相关参数。

#### 15.7 样本失衡会对SVM的结果产生影响吗？
红色直线为分割线，蓝色直线为支持向量。</br>
情形一、 线性可分的情况</br>
假设真实数据集如下：</br>
![真实数据分布1](https://images0.cnblogs.com/blog2015/735433/201507/111100166117391.png)

由于负类样本量太少，可能会出现下面这种情况：

![真实数据划分1](https://images0.cnblogs.com/blog2015/735433/201507/111105266582004.png)

使得分隔超平面偏向负类。严格意义上，这种样本不平衡不是因为样本数量的问题，而是因为边界点发生了变化。

情形二、 线性不可分的情况</br>
源数据以及理想的超平面情况如下：

![真实数据分布2](https://images0.cnblogs.com/blog2015/735433/201507/111126166276031.png)

很可能由于负类样本太少出现以下这种情况，超平面偏向负类:

![真实数据划分2](https://images0.cnblogs.com/blog2015/735433/201507/111130374557380.png)

解决不平衡的方案：</br>
首先需要明白，a.SVM对不平衡本身并不十分敏感；</br>
b. SVM的超平面只与支持向量有关，因此原离决策超平面的数据的多少并不重要；

方案：
1. 过采样和欠采样
2. 对正例和负例赋予不同的C值，例如正例远少于负例，则正例的C值取得较大，这种方法的缺点是可能会偏离原始数据的概率分布；
3. 基于核函数的不平衡数据处理。

#### 15.8 SVM适合处理什么样的数据？
高维稀疏，样本少。

首先，参数只与支持向量有关，数量少，所以需要的样本少；</br>
然后，由于参数跟维度没有关系，所以可以处理高维问题

参考：
1. [零基础学SVM-Support Vector Machine(一)](https://zhuanlan.zhihu.com/p/24638007)

1. [零基础学SVM-Support Vector Machine(二)](https://zhuanlan.zhihu.com/p/29865057)

1. [支持向量机通俗导论（理解SVM的三层境界）](https://blog.csdn.net/v_july_v/article/details/7624837 "支持向量机通俗导论（理解SVM的三层境界）")

1. [机器学习技法（林轩田）](https://www.bilibili.com/video/av12469267/?p=3 "机器学习技法（林轩田）")

1. [怎么样理解SVM中的hinge-loss？](https://www.zhihu.com/question/47746939/answer/154058298)

1. [刘建平:支持向量机原理(一) 线性支持向量机](http://www.cnblogs.com/pinard/p/6097604.html)

1. [如何通俗地讲解对偶问题？尤其是拉格朗日对偶lagrangian duality？](https://www.zhihu.com/question/58584814)

1. [支持向量机(SVM)是否适合大规模数据？](https://www.zhihu.com/question/19591450)

1. [SVM的核函数如何选取？](https://www.zhihu.com/question/21883548)

1. [Improvements to Platt’s SMO Algorithm](http://www.cnblogs.com/vivounicorn/archive/2011/08/25/2152824.html)

1. [样本失衡会对SVM的影响](http://www.cnblogs.com/xiangzhi/p/4638235.html)