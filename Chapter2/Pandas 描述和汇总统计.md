# Pandas 描述和汇总统计 

pandas 提供了很多常用的数学和统计方法，其中大部分都属于约简和汇总统计，用于从Series 中提取单个值（如sum或mean）或从DataFrame的行或列中提取一个 Series。

`mean()`平均值 `median()`中位数 `max()`最大值 `min()`最小值 `sum()`求和 `std()`标准差

Series类型独有的方法： `argmax()`最大值的位置 `argmin()`最小值的位置


## DataFrame的`sum`和`mean`方法

```python
a = [[1,np.nan,9],[2,8,3],[3,5,np.nan]]
data = DataFrame(a,index=["a","b","c"],columns=["one","two","three"])
print(data)
'''
one  two  three
a    1  NaN    9.0
b    2  8.0    3.0
c    3  5.0    NaN
'''
#对列求和
print(data.sum())
'''
one       6.0
two      13.0
three    12.0
'''
#对行求和
print(data.sum(axis=1))
'''
a    10.0
b    13.0
c     8.0
'''
#对行求平均值,默认排除NaN值
print(data.mean(axis=1))
'''
a    5.000000
b    4.333333
c    4.000000
'''
#对行求平均值，禁用自动排除NaN值
print(data.mean(axis=1,skipna=False))
'''
a         NaN
b    4.333333
c         NaN
'''

```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200501162055.png"/>

## 统计 `.idxmax()`, `.idxmin()`, `.cumsum()`

上面的操作都是对于列，如果想要对行进行操作，只需要在方法中设置axis参数为1即可。

```python
a = [[1,np.nan,9],[2,8,3],[3,5,np.nan]]
data = DataFrame(a,index=["0","1","2"],columns=["a","b","c"])
print(data)
'''
   a    b    c
0  1  NaN  9.0
1  2  8.0  3.0
2  3  5.0  NaN
'''

# 返回每一列中最大值的行索引
print(data.idxmax())
'''
a    2
b    1
c    0
dtype: object
'''

#返回每一列中最小值的行索引
print(data.idxmin())
'''
a    0
b    2
c    1
dtype: object
'''

#对每列的值进行累加
print(data.cumsum())
'''
     a     b     c
0  1.0   NaN   9.0
1  3.0   8.0  12.0
2  6.0  13.0   NaN
'''

```

## 数据描述

### **DataFrame**

#### **`df.describe()`**

```python
a = [[1,np.nan,9],[2,8,3],[3,5,np.nan]]
data = DataFrame(a,index=["0","1","2"],columns=["a","b","c"])
print(data)
'''
a    b    c
0  1  NaN  9.0
1  2  8.0  3.0
2  3  5.0  NaN
'''
#列出DataFrame的描述
'''
四分位数用于绘制箱线图判断是否为异常值
count：该列（行）非NA值的个数
mean ：该列（行）的均值
std  ：该列（行）的方差
25%  ：上四分位数
50%  ：非NA值的平均数
75%  ：下四分位数
max  ：最大值
'''
print(data.describe())
'''
a        b         c
count  3.0  2.00000  2.000000
mean   2.0  6.50000  6.000000
std    1.0  2.12132  4.242641
min    1.0  5.00000  3.000000
25%    1.5  5.75000  4.500000
50%    2.0  6.50000  6.000000
75%    2.5  7.25000  7.500000
max    3.0  8.00000  9.000000    
'''

```

### Series

如果值是数值型的描述与DataFrame一致，

```python
s = Series(["a","b","b","d"])
print(s)
'''
0    a
1    b
2    b
3    d
'''
print(s.describe())
'''
count     4
unique    3
top       b
freq      2
'''

```

## `argmax()`, `argmin()`,`.tolist()`



`argmax()`某一列最大值的位置 `argmin()`最小值的位置,`.tolist()` tolist()转换成list类型

```python
# coding=utf-8
import numpy as np
import pandas as pd
 
 
# 创建DataFrame
df = pd.DataFrame(np.arange(12, 32).reshape((5, 4)), index=["a", "b", "c", "d", "e"], columns=["WW", "XX", "YY", "ZZ"])
print(df)
'''
   WW  XX  YY  ZZ
a  12  13  14  15
b  16  17  18  19
c  20  21  22  23
d  24  25  26  27
e  28  29  30  31
'''
 
 
# mean()平均值  median()中位数  max()最大值  min()最小值  sum()求和  std()标准差
print(df.mean())  # 每一列平均值 (Series类型)
'''
WW    20.0
XX    21.0
YY    22.0
ZZ    23.0
dtype: float64
'''
 
print(df["YY"].mean())  # 22.0  指定列的平均值
 
print(df["YY"])  # Series类型
YY_list = df["YY"].tolist()  # tolist()转换成list类型
print(YY_list)  # [14, 18, 22, 26, 30]
print(len(YY_list))  # 5
print(len(set(YY_list)))  # set集合可以去重
 
print(df["YY"].unique())  # [14 18 22 26 30]  unique()自动去重(ndarray类型)
 
 
print(df.max())  # 每一列的最大值 Series类型。  min()最小值
'''
WW    28
XX    29
YY    30
ZZ    31
dtype: int64
'''
 
# argmax()某一列最大值的位置  argmin()最小值的位置
print(df["YY"].argmax())  # e
 

```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200501162644.png"/>

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200501162859.png"/>