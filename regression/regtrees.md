### ID3
#### 1.1.1 ID3原理
**原理**：每次选取当前最佳的特征来分割数据，并按照该特征的所有可能取值来切分。

#### 1.2.1 ID3 缺陷:切分方式过于迅速
也就是说，如果一个特征有 4 种取值，那么数据将被切分成 4 份。一旦按照某特征切分后，该特征在之后的算法执行过程中将不会再起作用，所以有观点认为这种**切分方式过于迅速**。

#### 1.2.2 ID3 缺陷: 不能直接处理连续型特征
只有事先将连续型特征转换成离散型，才能在 ID3 算法中使用。但这种转换过程会破坏连续型变量的内在性质。

#### 1.3 二元切分法
另外一种方法是二元切分法，即每次把数据集切分成两份。如果数据的某特征值等于切分所要求的值，那么这些数据就进入树的左子树，反之则进入树的右子树。另外，二元切分法也节省了树的构建时间，但这点意义也不是特别大，因为这些树构建一般是离线完成，时间并非需要重点关注的因素。

### 划分分支方式
- ID3 是信息增益分支
- C4.5 是信息增益率分支
- CART 做分类工作时，采用 GINI 值作为节点分裂的依据；回归时，采用样本的最小方差作为节点的分裂依据。

**工程上总的来说**:
CART 和 C4.5 之间主要差异在于分类结果上，CART 可以回归分析也可以分类，C4.5 只能做分类；C4.5 子节点是可以多分的，而 CART 是无数个二叉子节点；