# rolling滚动计算函数

## `Rolling.count()`

窗口内任何非NaN观测值的滚动计数

```python
>>> s = pd.Series([2, 3, np.nan, 10])
>>> s.rolling(2).count()
0    1.0
1    2.0
2    1.0
3    1.0
dtype: float64
>>> s.rolling(3).count()
0    1.0
1    2.0
2    2.0
3    2.0
dtype: float64
>>> s.rolling(4).count()
0    1.0
1    2.0
2    2.0
3    3.0
dtype: float64
```

## `Rolling.sum`

计算给定DataFrame或Series的滚动总和

```python
>>> s = pd.Series([1, 2, 3, 4, 5])
>>> s
0    1
1    2
2    3
3    4
4    5
dtype: int64
```

```python
>>> s.rolling(3).sum()
0     NaN
1     NaN
2     6.0
3     9.0
4    12.0
dtype: float64

>>> s.expanding(3).sum()
0     NaN
1     NaN
2     6.0
3    10.0
4    15.0
dtype: float64

>>> s.rolling(3, center=True).sum()
0     NaN
1     6.0
2     9.0
3    12.0
4     NaN
dtype: float64
```

## `Rolling.median`

计算滚动中位数。

```
Rolling.median(self, **kwargs)
```

```python
>>> s = pd.Series([0, 1, 2, 3, 4])
>>> s.rolling(3).median()
0    NaN
1    NaN
2    1.0
3    2.0
4    3.0
dtype: float64
```

## `Rolling.var`

计算无偏滚动方差。

```
Rolling.var(self, ddof=1, *args, **kwargs)

ddof : int, default 1
	   Delta Degrees of Freedom. The divisor used in calculations is N - ddof, 
	   where N represents the number of elements.

*args, **kwargs
		For NumPy compatibility. No additional arguments are used.

```

```python
>>> s = pd.Series([5, 5, 6, 7, 5, 5, 5])
>>> s.rolling(3).var()
0         NaN
1         NaN
2    0.333333
3    1.000000
4    1.000000
5    1.333333
6    0.000000
dtype: float64

>>> s.expanding(3).var()
0         NaN
1         NaN
2    0.333333
3    0.916667
4    0.800000
5    0.700000
6    0.619048
dtype: float64
```

## Rolling.std

计算滚动标准偏差。

## Rolling.min

计算滚动最小值。

## Rolling.max

计算滚动最大值。

## Rolling.corr

计算滚动相关系数

```
Rolling.corr(self, other=None, pairwise=None, **kwargs)

other : Series, DataFrame, or ndarray, optional
		If not supplied then will default to self.

pairwise : bool, default None
		   Calculate pairwise combinations of columns within a DataFrame. 
		   If other is not specified, defaults to True, 
		   otherwise defaults to False. Not relevant for Series.

**kwargs
		Unused.
```

```python
>>> v1 = [3, 3, 3, 5, 8]
>>> v2 = [3, 4, 4, 4, 8]

>>> s1 = pd.Series(v1) 
>>> s2 = pd.Series(v2)
>>> s1.rolling(4).corr(s2)
0         NaN
1         NaN
2         NaN
3    0.333333
4    0.916949
dtype: float64
```

使用pairwise选项对DataFrame进行类似的滚动计算

```python
>>> matrix = np.array([[51., 35.], [49., 30.], [47., 32.],    [46., 31.], [50., 36.]])
>>> df = pd.DataFrame(matrix, columns=['X','Y'])
>>> df
      X     Y
0  51.0  35.0
1  49.0  30.0
2  47.0  32.0
3  46.0  31.0
4  50.0  36.0
>>> df.rolling(4).corr(pairwise=True)
            X         Y
0 X       NaN       NaN
  Y       NaN       NaN
1 X       NaN       NaN
  Y       NaN       NaN
2 X       NaN       NaN
  Y       NaN       NaN
3 X  1.000000  0.626300
  Y  0.626300  1.000000
4 X  1.000000  0.555368
  Y  0.555368  1.000000
# 索引为 3 和 4 的两个矩阵, 右下对角线为自身的相关系数，右上对角线为两者的相关系数
```

## Rolling.cov

计算滚动样本协方差

```
Rolling.cov(self, other=None, pairwise=None, ddof=1, **kwargs)
```