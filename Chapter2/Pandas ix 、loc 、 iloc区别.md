# Pandas ix 、loc 、 iloc区别 

##  `loc`

### `loc`——通过行标签索引行数据

`loc[1]`表示索引的是第1行（ index 是整数）

`.loc`主要是基于标签(label)的，包括行标签(index)和列标签(columns)，即行名称和列名称，可以使用`df.loc[index_name,col_name]`，选择指定位置的数据

- **使用单个标签**

如果`.loc[]`中只有单个标签，那么选择的是某一行。 `df.loc[1]`选择的是 index 名为 ‘1’ 的一行，注意这里的’1’是index的名称，而不是序号



```python
data = [[1,2,3],[4,5,6]]
index = [0,1]
columns=['a','b','c']
df = pd.DataFrame(data=data, index=index, columns=columns)

df

	a	b	c
0	1	2	3
1	4	5	6
 
# 选取行号为 1 的 index
df.loc[1]
a    4
b    5
c    6
Name: 1, dtype: int64
```

- **使用标签的list**：同样是只选择行

```python
df.loc[[0,1]]


	a	b	c
0	1	2	3
1	4	5	6
```

- **标签的切片对象**：与通常的python切片不同，在最终选择的数据中包含切片的**start** 和 **stop**

```python
df.loc['c':'f']

	A			B			C			D
c	0.546339	0.009044	0.774770	0.121425
d	0.517394	0.665752	0.762913	0.940879
e	0.123988	0.209996	0.365368	0.401288
f	0.590005	0.993915	0.611509	0.683021
```

- **布尔型的数组**：通常用于筛选符合某些条件的行

```
df.loc[df.A > 0.7]


	A			B		C			D
a	0.899727	0.61540	0.970942	0.621620
b	0.936262	0.59904	0.139279	0.678375
```

A 属性大于 0.7 的所有 C 和 D 列

```python
df.loc[df.A > 0.7,['C', 'D']]

	C			D
a	0.970942	0.621620
b	0.139279	0.678375
```

- **可调用的函数**

```python
df.loc[lambda df : df.A > 0.7]
	A			B		C			D
a	0.899727	0.61540	0.970942	0.621620
b	0.936262	0.59904	0.139279	0.678375
```

`lambda`表达式语法：
lambda 传入参数 ： 返回的计算表达式

###  loc扩展——索引某行某列

**索引某行某列**

```python
data = [[1,2,3],[4,5,6]]
index = ['d','e']
columns=['a','b','c']
df = pd.DataFrame(data=data, index=index, columns=columns)
print(df)
'''
   a  b  c
d  1  2  3
e  4  5  6
'''
print (df.loc['d',['b','c']])
'''
b    2
c    3
'''

```

**索引某列**

```python
import pandas as pd
data = [[1,2,3],[4,5,6]]
index = ['d','e']
columns=['a','b','c']
df = pd.DataFrame(data=data, index=index, columns=columns)
print(df)
'''
   a  b  c
d  1  2  3
e  4  5  6
'''
print (df.loc[:,['c']])
'''
   c
d  3
e  6
'''


df = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
     index=['cobra', 'viper', 'sidewinder'],
      columns=['max_speed', 'shield'])
print(df)
print(df.loc[['viper', 'sidewinder'],['max_speed', 'shield']])
'''
            max_speed  shield
cobra               1       2
viper               4       5
sidewinder          7       8
            
            max_speed  shield
viper               4       5
sidewinder          7       8

'''

```

## `iloc`用法

`iloc`是基于位置的索引，利用元素在各个轴上的索引序号进行选择，序号超出范围会产生`IndexError`，切片时允许序号超过范围，用法包括：

- **使用整数**：与`.loc`相同，如果只使用一个维度，则对行选择，下标从0开始

```python
# 选择第六行数据
df.iloc[5]

A    0.590005
B    0.993915
C    0.611509
D    0.683021
Name: f, dtype: float64
```

- **使用列表或数组**，同样是对行选择

```python
df.iloc[[1,3,4]]


	A			B			C			D
b	0.936262	0.599040	0.139279	0.678375
d	0.517394	0.665752	0.762913	0.940879
e	0.123988	0.209996	0.365368	0.401288
```



- **元素为整数的切片对象**：与`.loc`不同的是，这里下标为`stop`的数据不被选择

```python
df.iloc[0:3]

	A			B			C			D
a	0.899727	0.615400	0.970942	0.621620
b	0.936262	0.599040	0.139279	0.678375
c	0.546339	0.009044	0.774770	0.121425
```



也可以对列进行切片：

```python
df.iloc[0:3,1:3]


	B			C
a	0.615400	0.970942
b	0.599040	0.139279
c	0.009044	0.774770


import pandas as pd
data = [[1,2,3],[4,5,6]]
index = ['d','e']
columns=['a','b','c']
df = pd.DataFrame(data=data, index=index, columns=columns)
print(df)
'''
   a  b  c
d  1  2  3
e  4  5  6
'''
print (df.iloc[:,[1]])
'''
   b
d  2
e  5
'''

```



- **使用布尔数组进行筛选**：
  注意这里可以使用 list 或者 array，使用 Series 的话会出错，NotImplementedError或者ValueError，前者是Series的index与待切片DataFrame的index不同时，后者是index相同时报的错，可以自己实现体会一下。与.loc使用布尔数组，可以使用list， array，也可以使用Series，使用Series时index需要一致，否则会报IndexingError

```python
df.iloc[np.array(df.A > 0.6)]


	A			B		C			D
a	0.899727	0.61540	0.970942	0.621620
b	0.936262	0.59904	0.139279	0.678375
```

- **使用可调用函数**

```python
df.iloc[lambda df : [0,1]]  # 选择前两行

	A			B		C			D
a	0.899727	0.61540	0.970942	0.621620
b	0.936262	0.59904	0.139279	0.678375
```

## `ix`——结合前两种的混合索引

### 通过行号索引

```python
df.ix[0]

A    0.899727
B    0.615400
C    0.970942
D    0.621620
Name: a, dtype: float64
```

### 通过行标签索引

```python
df.ix['a']

A    0.899727
B    0.615400
C    0.970942
D    0.621620
Name: a, dtype: float64
```

## 切片操作`[]`

`[]`操作只能输入一个维度，不能用逗号隔开输入两个维度：

- **使用列名**：`.loc`和`iloc`只输入一维时选取的是行，**而`[]`选取的是列，并且必须使用列名**

```python
df[['A','B']]

	A			B
a	0.899727	0.615400
b	0.936262	0.599040
c	0.546339	0.009044
d	0.517394	0.665752
e	0.123988	0.209996
f	0.590005	0.993915
```

- **用布尔数组**：bool 数组的 index 需要和 dataframe 的 index 一致，**此时选取的是行**

```python
df[df.B > 0.6]


	A			B			C			D
a	0.899727	0.615400	0.970942	0.621620
d	0.517394	0.665752	0.762913	0.940879
f	0.590005	0.993915	0.611509	0.683021
```

`.a`、`.iat`与`loc` 、`iloc`类似，`.a`、`loc` 、只能通过标签获取值，`.iat`、`iloc`通过行号，列号获取值

```python
df = pd.DataFrame([[0, 2, 3], [0, 4, 1], [10, 20, 30]],
                   columns=['A', 'B', 'C'])
print(df)
'''
    A   B   C
0   0   2   3
1   0   4   1
2  10  20  30
'''
print(df.at[2, 'B'])
#20

print(df.at[2, 2])
#ValueError: At based indexing on an non-integer index can only have non-integer indexers

print(df.get_value(2,'B'))
#20

print(df.get_value(2,2))
#只能根据标签索引

```



参考：

<a href="[https://blog.csdn.net/flyfish5/article/details/79852938#loc%E7%94%A8%E6%B3%95](https://blog.csdn.net/flyfish5/article/details/79852938#loc用法)" blank="">pandas索引和选择数据</a> 

<a href="https://blog.csdn.net/chenKFKevin/article/details/62049060" blank="">python选取特定列——pandas的iloc和loc以及icol使用</a> 