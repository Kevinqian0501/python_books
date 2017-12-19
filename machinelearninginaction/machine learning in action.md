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





