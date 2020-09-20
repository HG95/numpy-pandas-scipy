# Pandas transform函数

```
DataFrame.transform(func, axis=0, *args, **kwargs)
```

参数

- **func** : `function`, `str`, `list` 或 `dict`

  用于转换数据的函数。如果是函数，则必须在传递`DataFrame`

  或传递到`DataFrame.apply`时工作

- **axis** : {0 or ‘index’, 1 或 ‘columns’}, 默认 0

  如果0或' index ':应用函数到每一列。

  如果1或‘columns’:应用函数到每一行。

返回值：**DataFrame**  必须具有与自身相同长度的`DataFrame`。

**特点**

`transform` 方法通常是和 `groupby` 方法一起连用的

- 产生一个标量值，并且广播到各分组的尺寸数据中
- `transform`可以产生一个和输入尺寸相同的对象
- `transform`不可改变它的输入

**例子**，

```python
>>> df = pd.DataFrame({'A': range(3), 'B': range(1, 4)})
>>> df
   A  B
0  0  1
1  1  2
2  2  3
>>> df.transform(lambda x: x + 1)
   A  B
0  1  2
1  2  3
2  3  4
```

**即使得到的DataFrame必须与输入DataFrame具有相同的长度，也可以提供几个输入函数**:

```
>>> s = pd.Series(range(3))
>>> s
0    0
1    1
2    2
dtype: int64
>>> s.transform([np.sqrt, np.exp])
       sqrt        exp
0  0.000000   1.000000
1  1.000000   2.718282
2  1.414214   7.389056
```



2 

```python
df = pd.DataFrame({
    "key":["a","b","c"]*2 ,
    "values":np.arange(6)
})
df

	key	values
0	a	0
1	b	1
2	c	2
3	a	3
4	b	4
5	c	5

```

分组

```python
g = df.groupby("key").values  # 分组再求平均
g.mean()

key
a    1.5
b    2.5
c    3.5
Name: values, dtype: float64
```

transform使用

每个位置被均值取代

```
g.transform(lambda x:x.mean())
0    1.5
1    2.5
2    3.5
3    1.5
4    2.5
5    3.5
Name: values, dtype: float64
```

传递agg方法中的函数字符串别名

内建的聚合函数直接传递别名，max\min\sum\mean

```python
g.transform("mean")
0    1.5
1    2.5
2    3.5
3    1.5
4    2.5
5    3.5
Name: values, dtype: float64
```

降序排名

```python
g.transform(lambda x:x.rank(ascending=False))

0    2
1    2
2    2
3    1
4    1
5    1
Name: values, dtype: int32
```



# transform 函数和 apply 函数的区别

### transform 函数：

> ​           1.只允许在同一时间在一个Series上进行一次转换，如果定义列‘a’ 减去列‘b’， 则会出现异常；
>
> ​           2.必须返回与 group相同的单个维度的序列（行）
>
> ​           \3. 返回单个标量对象也可以使用，如 . transform(sum)

 

### apply函数：

> ​          \1. 不同于transform只允许在Series上进行一次转换， apply对整个DataFrame 作用
>
> ​           2.apply隐式地将group 上所有的列作为自定义函数

### 栗子：

```
#coding=gbk
import numpy as np
import pandas as pd
data  = pd.DataFrame({'state':['Florida','Florida','Texas','Texas'],
                      'a':[4,5,1,3],
                      'b':[6,10,3,11]
                      })
print(data)
#    a   b    state
# 0  4   6  Florida
# 1  5  10  Florida
# 2  1   3    Texas
# 3  3  11    Texas
def sub_two(X):
    return X['a'] - X['b']
data1 = data.groupby(data['state']).apply(sub_two) # 此处使用transform 则会出现错误
print(data1)
# state     
# Florida  0   -2
#          1   -5
# Texas    2   -2
#          3   -8
# dtype: int64
```

返回单个标量可以使用transform：

：我们可以看到使用transform 和apply 的输出结果形式是不一样的，transform返回与数据同样长度的行，而apply则进行了聚合

此时，使用apply说明的信息更明确

```python
np.random.seed(666)
df = pd.DataFrame({'A' : ['foo', 'bar', 'foo', 'bar',
                          'foo', 'bar', 'foo', 'foo'],
                   'B' : ['one', 'one', 'two', 'three',
                         'two', 'two', 'one', 'three'],
                   'C' : np.random.randn(8), 'D' : np.random.randn(8)})
print(df)
#      A      B         C         D
# 0  foo    one  0.824188  0.640573
# 1  bar    one  0.479966 -0.786443
# 2  foo    two  1.173468  0.608870
# 3  bar  three  0.909048 -0.931012
# 4  foo    two -0.571721  0.978222
# 5  bar    two -0.109497 -0.736918
# 6  foo    one  0.019028 -0.298733
# 7  foo  three -0.943761 -0.460587
def zscore(x):
    return (x - x.mean())/ x.var()  
print(df.groupby('A').transform(zscore))  #自动识别CD列
print(df.groupby('A')['C','D'].apply(zscore))   #此种形式则两种输出数据是一样的
# df.groupby('A').apply(zscore)  此种情况则会报错，apply对整个dataframe作用
 
df['sum_c'] = df.groupby('A')['C'].transform(sum)   #先对A列进行分组， 计算C列的和
df = df.sort_values('A')
print(df)
#      A      B         C         D     sum_c
# 1  bar    one  0.479966 -0.786443  1.279517
# 3  bar  three  0.909048 -0.931012  1.279517
# 5  bar    two -0.109497 -0.736918  1.279517
# 0  foo    one  0.824188  0.640573  0.501202
# 2  foo    two  1.173468  0.608870  0.501202
# 4  foo    two -0.571721  0.978222  0.501202
# 6  foo    one  0.019028 -0.298733  0.501202
# 7  foo  three -0.943761 -0.460587  0.501202
print(df.groupby('A')['C'].apply(sum))
# A
# bar    1.279517
# foo    0.501202
# Name: C, dtype: float64
```

参考

- <a href="https://blog.csdn.net/qq_40587575/article/details/81204514" target="_blank">pandas中 transform 函数和 apply 函数的区别</a>