# Chapter2: k-近邻算法
- 优点:精度高、对异常值不敏感、无数据输入假定。
- 缺点:计算复杂度高、空间复杂度高。
- 适用数据范围:数值型和标称型。

k-近邻算法是分类数据最简单最有效的算法，本章通过两个例子讲述了如何使用k-近邻算法 构造分类器。k-近邻算法是基于实例的学习，使用算法时我们必须有接近实际数据的训练样本数 据。k-近邻算法必须保存全部数据集，如果训练数据集的很大，必须使用大量的存储空间。此外， 由于必须对数据集中的每个数据计算距离值，实际使用时可能非常耗时。
k-近邻算法的另一个缺陷是它无法给出任何数据的基础结构信息，因此我们也无法知晓平均 实例样本和典型实例样本具有什么特征。下一章我们将使用概率测量方法处理分类问题，该算法 可以解决这个问题。

# Chapter3: Decision tree
- 优点:计算复杂度不高，输出结果易于理解，对中间值的缺失不敏感，可以处理不相关特 征数据。
- 缺点:可能会产生过度匹配问题。
适用数据类型:数值型和标称型。

### ID3 (Examples, Target_Attribute, Attributes)
```
    Create a root node for the tree
    If all examples are positive, Return the single-node tree Root, with label = +.
    If all examples are negative, Return the single-node tree Root, with label = -.
    If number of predicting attributes is empty, then Return the single node tree Root,
    with label = most common value of the target attribute in the examples.
    Otherwise Begin
        A ← The Attribute that best classifies examples.
        Decision Tree attribute for Root = A.
        For each possible value, vi, of A,
            Add a new tree branch below Root, corresponding to the test A = vi.
            Let Examples(vi) be the subset of examples that have the value vi for A
            If Examples(vi) is empty
                Then below this new branch add a leaf node with label = most common target value in the examples
            Else below this new branch add the subtree ID3 (Examples(vi), Target_Attribute, Attributes – {A})
    End
    Return Root
```

### C4.5 algorithm

```
 1. Check for the above base cases.
 2. For each attribute a, find the normalized information gain ratio from splitting on a.
 3. Let a_best be the attribute with the highest normalized information gain.
 4. Create a decision node that splits on a_best.
 5. Recur on the sublists obtained by splitting on a_best, and add those nodes as children of node.
```
C4.5 made a number of improvements to ID3. Some of these are:

- Handling both continuous and discrete attributes - In order to handle continuous attributes, C4.5 creates a threshold and then splits the list into those whose attribute value is above the threshold and those that are less than or equal to it.[5]
- Handling training data with missing attribute values - C4.5 allows attribute values to be marked as ? for missing. Missing attribute values are simply not used in gain and entropy calculations.
- Handling attributes with differing costs.
- Pruning trees after creation - C4.5 goes back through the tree once it's been created and attempts to remove branches that do not help by replacing them with leaf nodes.


### Pruning tree
- [Decision Tree：CART、剪枝](http://isilic.iteye.com/blog/1846726)

# Chapter4: Naive Bayes

- 优点:在数据较少的情况下仍然有效，可以处理多类别问题。
- 缺点:对于输入数据的准备方式较为敏感。
适用数据类型:标称型数据。

对于分类而言，使用概率有时要比使用硬规则更为有效。贝叶斯概率及贝叶斯准则提供了一 种利用已知值来估计未知概率的有效方法。
可以通过特征之间的条件独立性假设，降低对数据量的需求。独立性假设是指一个词的出现概率并不依赖于文档中的其他词。当然我们也知道这个假设过于简单。这就是之所以称为朴素贝 叶斯的原因。尽管条件独立性假设并不正确，但是朴素贝叶斯仍然是一种有效的分类器。


# Chapter5: Logistic Regression
  
- 优点:计算代价不高，易于理解和实现。
- 缺点:容易欠拟合，分类精度可能不高。
适用数据类型:数值型和标称型数据。

# Chapter6: SVM

- 优点:泛化错误率低，计算开销不大，结果易解释。
- 缺点:对参数调节和核函数的选择敏感，原始分类器不加修改仅适用于处理二类问题。
适用数据类型:数值型和标称型数据。


# Chapter7: AdaBoost
[*Adaboost 算法的原理与推导*](http://blog.csdn.net/v_july_v/article/details/40718799)
  
- 优点:泛化错误率低，易编码，可以应用在大部分分类器上，无参数调整。
- 缺点:对离群点敏感。
适用数据类型:数值型和标称型数据。

### 非均衡分类问题
#### 其他分类性能度量指标:正确率、召回率及 ROC 曲线
在分类中，当某个类别的重要性高于其他类别时，我们就可以利用上述定义来定义出多个比错误率更好的新指标。第一个指标是正确率(Precision)，它等于TP/(TP+FP)，给出的是预测为正例的 样本中的真正正例的比例。第二个指标是召回率(Recall)，它等于TP/(TP+FN)，给出的是预测为正 例的真实正例占所有真实正例的比例。在召回率很大的分类器中，真正判错的正例的数目并不多。

ROC曲线不但可以用于比较分类器，还可以基于成本效益(cost-versus-benefit)分析来做出 决策。由于在不同的阈值下，不同的分类器的表现情况可能各不相同，因此以某种方式将它们组 合起来或许会更有意义。如果只是简单地观察分类器的错误率，那么我们就难以得到这种更深入 的洞察效果了。

#### 基于代价函数的分类器决策控制
除了调节分类器的阈值之外，我们还有一些其他可以用于处理非均匀分类代价问题的方法， 其中的一种称为代价敏感的学习(cost-sensitive learning)。考虑表7-4中的代价矩阵，第一张表给 出的是到目前为止分类器的代价矩阵(代价不是0就是1)。我们可以基于该代价矩阵计算其总代 价:TP*0+FN*1+FP*1+TN*0。接下来我们考虑下面的第二张表，基于该代价矩阵的分类代价的 计算公式为:TP*(-5)+FN*1+FP*50+TN*0。采用第二张表作为代价矩阵时，两种分类错误的代 价是不一样的。类似地，这两种正确分类所得到的收益也不一样。如果在构建分类器时，知道了 这些代价值，那么就可以选择付出最小代价的分类器。
在分类算法中，我们有很多方法可以用来引入代价信息。在AdaBoost中，可以基于代价函数 来调整错误权重向量D。在朴素贝叶斯中，可以选择具有最小期望代价而不是最大概率的类别作 为最后的结果。在SVM中，可以在代价函数中对于不同的类别选择不同的参数C。上述做法就会 给较小类更多的权重，即在训练时，小类当中只允许更少的错误。

#### 处理非均衡问题的数据抽样方法
另外一种针对非均衡问题调节分类器的方法，就是对分类器的训练数据进行改造。这可以通 过欠抽样(undersampling)或者过抽样(oversampling)来实现。过抽样意味着复制样例，而欠 抽样意味着删除样例。不管采用哪种方式，数据都会从原始形式改造为新形式。抽样过程则可以 通过随机方式或者某个预定方式来实现。
通常也会存在某个罕见的类别需要我们来识别，比如在信用卡欺诈当中。如前所述，正例类 别属于罕见类别。我们希望对于这种罕见类别能尽可能保留更多的信息，因此，我们应该保留正 例类别中的所有样例，而对反例类别进行欠抽样或者样例删除处理。这种方法的一个缺点就在于 要确定哪些样例需要进行剔除。但是，在选择剔除的样例中可能携带了剩余样例中并不包含的有 价值信息。
上述问题的一种解决办法，就是选择那些离决策边界较远的样例进行删除。假定我们有一个 数据集，其中有50例信用卡欺诈交易和5000例合法交易。如果我们想要对合法交易样例进行欠抽 样处理，使得这两类数据比较均衡的话，那么我们就需要去掉4950个样例，而这些样例中可能包 含很多有价值的信息。这看上去有些极端，因此有一种替代的策略就是使用反例类别的欠抽样和 正例类别的过抽样相混合的方法。
要对正例类别进行过抽样，我们可以复制已有样例或者加入与已有样例相似的点。一种方法 是加入已有数据点的插值点，但是这种做法可能会导致过拟合的问题。
