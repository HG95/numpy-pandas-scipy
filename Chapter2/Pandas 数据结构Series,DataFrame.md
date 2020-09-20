# Pandas 数据结构Series,DataFrame 

pandas 是基于 numpy 构建的，为时间序列分析提供了很好的支持。pandas中有两个主要的数据结构，一个是`Series`，另一个是`DataFrame`。

## Series

Series 类似于一维数组与字典(map)数据结构的结合。它由一组数据和一组与数据相对应的数据标签（索引index）组成。这组数据和索引标签的基础都是一个一维ndarray数组。可将index索引理解为行索引。

Series 的表现形式为：索引在左，数据在右。

```python
pd.Series(data, index=index)
```

`data` 支持以下数据类型：

- Python 字典
- 多维数组
- 标量值（如，5）

`index` 是轴标签列表。不同**数据**可分为以下几种情况：

**多维数组**

`data` 是多维数组时，**index** 长度必须与 **data** 长度一致。没有指定 `index` 参数时，创建数值型索引，即 `[0, ..., len(data) - 1]`。

```python
In [3]: s = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])

In [4]: s
Out[4]: 
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
e    1.212112
dtype: float64

In [5]: s.index
Out[5]: Index(['a', 'b', 'c', 'd', 'e'], dtype='object')

In [6]: pd.Series(np.random.randn(5))
Out[6]: 
0   -0.173215
1    0.119209
2   -1.044236
3   -0.861849
4   -2.104569
dtype: float64
```

**字典**

Series 可以用字典实例化：

```python
In [7]: d = {'b': 1, 'a': 0, 'c': 2}

In [8]: pd.Series(d)
Out[8]: 
b    1
a    0
c    2
dtype: int64
```

> `data` 为字典，且未设置 `index` 参数时，如果 Python 版本 >= 3.6 且 Pandas 版本 >= 0.23，`Series` 按字典的插入顺序排序索引。
>
> Python < 3.6 或 Pandas < 0.23，且未设置 `index` 参数时，`Series` 按字母顺序排序字典的键（key）列表。

> Pandas 用 `NaN`（Not a Number）表示**缺失数据**。



**标量值**

`data` 是标量值时，必须提供索引。`Series` 按**索引**长度重复该标量值。

```python
In [12]: pd.Series(5., index=['a', 'b', 'c', 'd', 'e'])
Out[12]: 
a    5.0
b    5.0
c    5.0
d    5.0
e    5.0
dtype: float64
```

### Series 类似多维数组

`Series` 操作与 `ndarray` 类似，支持大多数 NumPy 函数，还支持索引切片

```python
In [13]: s[0]
Out[13]: 0.4691122999071863

In [14]: s[:3]
Out[14]: 
a    0.469112
b   -0.282863
c   -1.509059
dtype: float64

In [15]: s[s > s.median()]
Out[15]: 
a    0.469112
e    1.212112
dtype: float64

In [16]: s[[4, 3, 1]]
Out[16]: 
e    1.212112
d   -1.135632
b   -0.282863
dtype: float64

In [17]: np.exp(s)
Out[17]: 
a    1.598575
b    0.753623
c    0.221118
d    0.321219
e    3.360575
dtype: float64
```

- 获取索引和数据：`ser_obj.index`, `ser_obj.values`

- 预览数据：`ser_obj.head(n)`, `ser_obj.tail(n)`

### 使用一维数组生成 Series





## DataFrame

**DataFrame** 是由多种类型的列构成的二维标签数据结构，类似于 Excel 、SQL 表，或 Series 对象构成的字典。DataFrame 是最常用的 Pandas 对象，与 Series 一样，DataFrame 支持多种类型的输入数据：

- 一维 ndarray、列表、字典、Series 字典
- 二维 numpy.ndarray
- [结构多维数组或记录多维数组](https://docs.scipy.org/doc/numpy/user/basics.rec.html)
- `Series`
- `DataFrame`

除了数据，还可以有选择地传递 **index**（行标签）和 **columns**（列标签）参数。传递了索引或列，就可以确保生成的 DataFrame 里包含索引或列。Series 字典加上指定索引时，会丢弃与传递的索引不匹配的所有数据。

> Python > = 3.6，且 Pandas > = 0.23，数据是字典，且未指定 `columns` 参数时，`DataFrame` 的列按字典的插入顺序排序.

### 用 Series 字典或字典生成 DataFrame

生成的**索引**是每个 **Series** 索引的并集。先把嵌套字典转换为 Series。如果没有指定列，DataFrame 的列就是字典键的有序列表。

```python
In [37]: d = {'one': pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
   ....:      'two': pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
   ....: 

In [38]: df = pd.DataFrame(d)

In [39]: df
Out[39]: 
   one  two
a  1.0  1.0
b  2.0  2.0
c  3.0  3.0
d  NaN  4.0

In [40]: pd.DataFrame(d, index=['d', 'b', 'a'])
Out[40]: 
   one  two
d  NaN  4.0
b  2.0  2.0
a  1.0  1.0

In [41]: pd.DataFrame(d, index=['d', 'b', 'a'], columns=['two', 'three'])
Out[41]: 
   two three
d  4.0   NaN
b  2.0   NaN
a  1.0   NaN
```

**index** 和 **columns** 属性分别用于访问行、列标签.

```python
In [42]: df.index
Out[42]: Index(['a', 'b', 'c', 'd'], dtype='object')

In [43]: df.columns
Out[43]: Index(['one', 'two'], dtype='object')
```

### 用多维数组字典、列表字典生成 DataFrame

多维数组的长度必须相同。如果传递了索引参数，`index` 的长度必须与数组一致。如果没有传递索引参数，生成的结果是 `range(n)`，`n` 为数组长度。

```python
In [44]: d = {'one': [1., 2., 3., 4.],
   ....:      'two': [4., 3., 2., 1.]}
   ....: 

In [45]: pd.DataFrame(d)
Out[45]: 
   one  two
0  1.0  4.0
1  2.0  3.0
2  3.0  2.0
3  4.0  1.0

In [46]: pd.DataFrame(d, index=['a', 'b', 'c', 'd'])
Out[46]: 
   one  two
a  1.0  4.0
b  2.0  3.0
c  3.0  2.0
d  4.0  1.0
```

### 用结构多维数组或记录多维数组生成 DataFrame

```python
In [47]: data = np.zeros((2, ), dtype=[('A', 'i4'), ('B', 'f4'), ('C', 'a10')])

In [48]: data[:] = [(1, 2., 'Hello'), (2, 3., "World")]

In [49]: pd.DataFrame(data)
Out[49]: 
   A    B         C
0  1  2.0  b'Hello'
1  2  3.0  b'World'

In [50]: pd.DataFrame(data, index=['first', 'second'])
Out[50]: 
        A    B         C
first   1  2.0  b'Hello'
second  2  3.0  b'World'

In [51]: pd.DataFrame(data, columns=['C', 'A', 'B'])
Out[51]: 
          C  A    B
0  b'Hello'  1  2.0
1  b'World'  2  3.0
```

### 用列表字典生成 DataFrame

```python
In [52]: data2 = [{'a': 1, 'b': 2}, {'a': 5, 'b': 10, 'c': 20}]

In [53]: pd.DataFrame(data2)
Out[53]: 
   a   b     c
0  1   2   NaN
1  5  10  20.0

In [54]: pd.DataFrame(data2, index=['first', 'second'])
Out[54]: 
        a   b     c
first   1   2   NaN
second  5  10  20.0

In [55]: pd.DataFrame(data2, columns=['a', 'b'])
Out[55]: 
   a   b
0  1   2
1  5  10
```

## 备选构建器

**DataFrame.from_dict**

```python
DataFrame.from_dict( data,
					 orient ='columns',
					 dtype = None,
					 columns = None 
					)

data:字典形式为{field：array-like}或{field：dict}。
    
orient:{‘columns’，‘index’}，默认’列’数据的“方向”。
    如果传递的dict的键应该是结果DataFrame的列，则传递’columns’（默认值）。
    否则，如果键应该是行，则传递’index’。

dtype：dtype:默认无数据类型强制，否则推断。

columns：list默认无要使用的列标签orient=‘index’。
	如果使用，则引发ValueError orient=‘columns’。
```



`DataFrame.from_dict` 接收字典组成的字典或数组序列字典，并生成 DataFrame。除了 `orient` 参数默认为 `columns`，本构建器的操作与 `DataFrame` 构建器类似。把 `orient` 参数设置为 `'index'`， 即可把字典的键作为行标签。

```python
In [57]: pd.DataFrame.from_dict(dict([('A', [1, 2, 3]), ('B', [4, 5, 6])]))
Out[57]: 
   A  B
0  1  4
1  2  5
2  3  6
```

`orient='index'` 时，键是行标签。本例还传递了列名：

```python
In [58]: pd.DataFrame.from_dict(dict([('A', [1, 2, 3]), ('B', [4, 5, 6])]),
   ....:                        orient='index', columns=['one', 'two', 'three'])
   ....: 
Out[58]: 
   one  two  three
A    1    2      3
B    4    5      6
```

