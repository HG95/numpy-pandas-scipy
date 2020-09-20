# DataFrame where

```python
DataFrame.where(cond, 
                other=nan, 
                inplace=False, 
                axis=None, 
                level=None, 
                errors='raise', 
                try_cast=False)
```

替换条件为假的值, 可以过滤不满足cond的值并赋予NaN空值

Parameters:

- **cond** : **bool Series/DataFrame, array-like, or callable**

  如果cond为True，请保留原始值。如果为False，则用其他的相应值替换。如果cond是可调用的，则它是在Series / DataFrame上计算的，并且应返回布尔Series / DataFrame或数组。可调用对象不得更改输入Series / DataFrame（尽管pandas不会对其进行检查）。

- **other** :scalar, Series/DataFrame, or callable

  Entries where cond is False are replaced with corresponding value from other. If other is callable, it is computed on the Series/DataFrame and should return scalar or Series/DataFrame. The callable must not change input Series/DataFrame (though pandas doesn’t check it).

- **inplace** :**bool, default False** 
  是否对数据执行适当的操作。

- **axis** :**int, default None**

- **level** :int, default None

  Alignment level if needed.

- **errors** :str, {‘raise’, ‘ignore’}, default ‘raise’

  Note that currently this parameter won’t affect the results and will always coerce to a suitable dtype.

  - ‘raise’ : allow exceptions to be raised.
  - ‘ignore’ : suppress exceptions. On error return original object.





**Examples**

返回大于 0 的值，不符合的用 NaN填充

```python
s = pd.Series(range(5))
s.where(s > 0)
0    NaN
1    1.0
2    2.0
3    3.0
4    4.0
dtype: float64
```

```python
s.mask(s > 0) # 与 where 的结果相反
0    0.0
1    NaN
2    NaN
3    NaN
4    NaN
dtype: float64
```

```
#返回大于 1 的值，不符合的用10填充
#cond = s > 1,other = 10
s.where(s > 1, 10) 
0    10
1    10
2    2
3    3
4    4
dtype: int64
```

```python
df = pd.DataFrame(np.arange(10).reshape(-1, 2), columns=['A', 'B'])
df
   A  B
0  0  1
1  2  3
2  4  5
3  6  7
4  8  9
m = df % 3 == 0
df.where(m, -df)
   A  B
0  0 -1
1 -2  3
2 -4 -5
3  6 -7
4 -8  9
df.where(m, -df) == np.where(m, df, -df)
      A     B
0  True  True
1  True  True
2  True  True
3  True  True
4  True  True
df.where(m, -df) == df.mask(~m, -df)
      A     B
0  True  True
1  True  True
2  True  True
3  True  True
4  True  True
```

去掉特定的某行某列：

```python
df.where(df !=N).dropna(axis = 1)
```



## DataFrame mask

与函数where<= ，相反的函数=>mask：where条件不符合进行替换，mask是条件符合进行替换。

```python
DataFrame.mask(self, 
               cond, 
               other=nan, 
               inplace=False,
               axis=None, 
               level=None, 
               errors='raise', 
               try_cast=False)

```

```python
s = pd.Series(range(5))
s.where(s > 0)
0    NaN
1    1.0
2    2.0
3    3.0
4    4.0
dtype: float64

#符合条件的替换 NaN
s.mask(s > 0)
0    0.0
1    NaN
2    NaN
3    NaN
4    NaN
dtype: float64


df = pd.DataFrame(np.arange(10).reshape(-1, 2), columns=['A', 'B'])
df
   A  B
0  0  1
1  2  3
2  4  5
3  6  7
4  8  9
m = df % 3 == 0
df.where(m, -df)
   A  B
0  0 -1
1 -2  3
2 -4 -5
3  6 -7
4 -8  9
df.where(m, -df) == np.where(m, df, -df)
      A     B
0  True  True
1  True  True
2  True  True
3  True  True
4  True  True
df.where(m, -df) == df.mask(~m, -df)
      A     B
0  True  True
1  True  True
2  True  True
3  True  True
4  True  True
```





## 与np.where的异同？

np.where(condition, [x, y]),这里三个参数,其中必写参数是condition(判断条件),后边的x和y是可选参数.那么这三个参数都有怎样的要求呢?

condition：array_like，bool ,当为True时，产生x，否则产生y

简单说,对第一个参数的要求是这样的,首先是数据类型的要求,类似于数组或者布尔值,当判断条件为真时返回x中的值,否则返回y中的值

x，y：array_like，可选,要从中选择的值。 x，y和condition需要可广播到某种形状

x和y是可选参数,并且对这两个参数的数据类型要求只有类似数组这一条,当条件判断为true或者false时从这两个类似数组的容器中取数.





参考

- <a href="https://www.cnblogs.com/wqbin/p/11777292.html" target=""> [pandas.DataFrame.where和mask 解读]</a>