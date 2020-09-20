# Pandas pd.Categorical()函数

```python
pandas.Categorical(values,
                   categories = None,
                   ordered = None,
                   dtype = Nonel
                   fastpath = False 
                  )
```

参数：

- values：类似列表。分类的值，如果给出了类别，则不在类别中的值将替换为NaN。
- categories：索引式（唯一），可选。此分类的唯一类别。如果没有给出，则假定类别是值的唯一值。
- ordered：布尔值，（默认为False）。这个分类是否被当作一个有序的分类。如果为True，产生的分类将是有序的。有序分类在排序时尊重其类别属性的顺序（如果提供了类别参数，则该属性也是类别参数
- dtype：CategoricalDtype，CategoricalDtype用于此分类的实例
  

示例

```python
import pandas as pd
cat = pd.Categorical(['a', 'b', 'c', 'a', 'b', 'c'])
cat
```

结果 ：

```
[a, b, c, a, b, c]
Categories (3, object): [a, b, c]
```

- 参数 `categories=`

```python
import pandas as pd
cat = cat=pd.Categorical(['a','b','c','a','b','c','d'], 
                         categories=['c', 'b', 'a'])
print (cat)
```

结果

```
[a, b, c, a, b, c, NaN]
Categories (3, object): [c, b, a]
```

在类别中不存在的任何值将被视为`NaN`

- 参数 `ordered`

```python
import pandas as pd
cat = cat=pd.Categorical(['a','b','c','a','b','c','d'], 
                         categories=['c', 'b', 'a'],
                         ordered=True)
print (cat)
```

结果：

```
[a, b, c, a, b, c, NaN]
Categories (3, object): [c < b < a]
```

从逻辑上讲，排序(*ordered*)意味着，`a`大于`b`，`b`大于`c`

这里就可以看到 categorical 实际上是计算一个列表型数据中的类别数，即不重复项，它返回的是一个CategoricalDtype 类型的对象，相当于在原来数据上附加上类别信息

**属性 ` codes `和 `categories `**

具体的类别可以通过和对应的序号可以通过` codes `和 `categories `来查看：

```python
In [23]: ss.codes
Out[23]: array([0, 0, 1, 2, 2], dtype=int8)

In [21]: ss.categories
Out[21]: Index(['a', 'b', 'c'], dtype='object')

```

有序分类可以根据类别的自定义顺序进行排序，并且可以具有最小值和最大值。

```python
>>>c = pd.Categorical(['a','b','c','a','b','c'], ordered=True, categories=['c', 'b', 'a'])
>>> c
[a, b, c, a, b, c]
Categories (3, object): [c < b < a]
>>> c.min()
'c'

```

属性

- `categories`	这种分类的类别。
- `codes`	此类别的类别代码。
- `ordered`	类别是否具有有序关系
- `dtype`	在CategoricalDtype此实例



## 参考

- <a href="https://blog.csdn.net/Lq_520/article/details/83616673" blank="">pandas 中 pd.Categorical用法</a>
- <a href="https://pandas.pydata.org/docs/reference/api/pandas.Categorical.html?highlight=categorical#pandas.Categorical"  target="_blank">pandas.Categorical</a> 
- <a href="https://www.yiibai.com/pandas/python_pandas_categorical_data.html"  target="_blank">Pandas分类数据</a>  

