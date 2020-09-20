# Pandas 唯一值，计数值 

## `unique()`

`pd.unique(Series)` 获取 Series 中元素的唯一值（即去掉重复的）

计算 Series 中的唯一值数组，按发现的顺序返回。

```python
obj=pd.Series(['c','a','d','a','a','b','b','c','c','c'])

print(obj.unique())
# ['c' 'a' 'd' 'b']

```

## `value_counts()`

`pd.value_counts(Series)` 统计 Series 中不同元素出现的次数

```python
print(obj.value_counts())
'''
c    4
a    3
b    2
d    1
dtype: int64
'''

```

## `isin()`

```python
In [144]: obj.isin(['a','b'])
Out[144]:
0    False
1     True
2    False
3     True
4     True
5     True
6     True
7    False
8    False
9    False
dtype: bool

```

## `pd.cut()`

```python
pandas.cut(x,
           bins,
           right=True,
           labels=None,
           retbins=False,
           precision=3,
           include_lowest=False
          )
```

参数

- `x `  : 进行划分的一维数组

- `bins` : bins 是被切割后的区间（或者叫“桶”、“箱”、“面元”），有3中形式：一个int型的标量、标量序列（数组）或者pandas.IntervalIndex 。
  - 一个int型的标量
    当bins为一个int型的标量时，代表将x平分成bins份。x的范围在每侧扩展0.1%，以包括x的最大值和最小值。
  - 标量序列
    标量序列定义了被分割后每一个bin的区间边缘，此时x没有扩展。
  - pandas.IntervalIndex
    定义要使用的精确区间 。
- ` right` : bool型参数，
  默认为True，表示是否包含区间右部。比如如果bins=[1,2,3]，right=True，则区间为(1,2]，(2,3]；right=False，则区间为(1,2),(2,3)。
- `labels`：给分割后的 bins 打标签，比如把年龄 x 分割成年龄段 bins 后，可以给年龄段打上诸如青年、中年的标签。
  labels 的长度必须和划分后的区间长度相等，比如bins=[1,2,3]，划分后有2个区间(1,2]，(2,3]，则labels的长度必须为2。如果指定 labels = False，则返回x中的数据在第几个bin中（从0开始）。
- `retbins`：bool 型的参数，表示是否将分割后的bins返回，当bins为一个int型的标量时比较有用，这样可以得到划分后的区间，默认为False。
-  `precision`: 保留区间小数点的位数，默认为3.
- `include_lowest` :bool型的参数，
  表示区间的左边是开还是闭的，默认为false，也就是不包含区间左部（闭）。

返回

- `out`：一个pandas.Categorical, Series或者ndarray类型的值，代表分区后x中的每个值在哪个bin（区间）中，如果指定了labels，则返回对应的label。
- `bins`：分隔后的区间，当指定retbins为True时返回。

```python
import numpy as np
import pandas as pd

# 年龄数据
ages = np.array([1,5,10,40,36,12,58,62,77,89,100,18,20,25,30,32])

# 将ages平分成5个区间
pd.cut(ages, 5)

[(0.901, 20.8], (0.901, 20.8], (0.901, 20.8], (20.8, 40.6], (20.8, 40.6], 
..., (0.901, 20.8], (0.901, 20.8], (20.8, 40.6], (20.8, 40.6], (20.8, 40.6]]
Length: 16
Categories (5, interval[float64]): [(0.901, 20.8] < (20.8, 40.6] 
              < (40.6, 60.4] < (60.4, 80.2] < (80.2, 100.0]]

```

可以看到 ages 被平分成 5 个区间，且区间两边都有扩展以包含最大值和最小值。

**将 ages 平分成 5 个区间并指定 labels**

```python
ages = np.array([1,5,10,40,36,12,58,62,77,89,100,18,20,25,30,32]) #年龄数据
pd.cut(ages, 5, labels=[u"婴儿",u"青年",u"中年",u"壮年",u"老年"])

[婴儿, 婴儿, 婴儿, 青年, 青年, ..., 婴儿, 婴儿, 青年, 青年, 青年]
Length: 16
Categories (5, object): [婴儿 < 青年 < 中年 < 壮年 < 老年]
```

**给ages指定区间进行分割**

```python
ages = np.array([1,5,10,40,36,12,58,62,77,89,100,18,20,25,30,32]) #年龄数据
pd.cut(ages, [0,5,20,30,50,100], labels=[u"婴儿",u"青年",u"中年",u"壮年",u"老年"])

[婴儿, 婴儿, 青年, 壮年, 壮年, ..., 青年, 青年, 中年, 中年, 壮年]
Length: 16
Categories (5, object): [婴儿 < 青年 < 中年 < 壮年 < 老年]

```

这里不再平分 ages，而是将 ages 分为了 5 个区间 (0, 5],(5, 20],(20, 30],(30,50],(50,100].

**返回分割后的 bins**

令`labels=False`即可

```python
ages = np.array([1,5,10,40,36,12,58,62,77,89,100,18,20,25,30,32]) #年龄数据
pd.cut(ages, [0,5,20,30,50,100], labels=False)

array([0, 0, 1, 3, 3, 1, 4, 4, 4, 4, 4, 1, 1, 2, 2, 3], dtype=int64)
```

参考

<a href="https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.cut.html" blank="">pandas.cut</a> 

<a href="https://www.cnblogs.com/sench/p/10128216.html" blank="">pandas.cut使用总结</a> 

