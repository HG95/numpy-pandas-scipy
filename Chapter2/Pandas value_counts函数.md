# Pandas value_counts()函数

```python
Series.value_counts(normalize=False, 
             sort=True, 
             ascending=False, 
             bins=None, dropna=True)
```

返回一个包含唯一值计数的系列。

pandas 的 `value_counts() `函数可以对Series里面的每个值进行计数并且排序。

## **Series 情况：**

```python
In [1]: import pandas as pd^M
   ...: df = pd.DataFrame({'区域' : ['西安', '太原', '西安', '太原', '郑州', '太原'], ^M
   ...:                   '10月份销售' : ['0.477468', '0.195046', '0.015964', '0.259654', '0.856412', '0.259644'],^M
   ...:                   '9月份销售' : ['0.347705', '0.151220', '0.895599', '0236547', '0.569841', '0.254784']})

In [2]: df
Out[2]:
   区域    10月份销售     9月份销售
0  西安  0.477468  0.347705
1  太原  0.195046  0.151220
2  西安  0.015964  0.895599
3  太原  0.259654   0236547
4  郑州  0.856412  0.569841
5  太原  0.259644  0.254784

# 统计每个区域出现多少次：
In [3]: df['区域'].value_counts()
Out[3]:
太原    3
西安    2
郑州    1
Name: 区域, dtype: int64
# 每个区域都被计数，并且默认从高到低排序。


# 如果想升序排列，设置参数 ascending = True：
In [4]: df['区域'].value_counts(ascending=True)
Out[4]:
郑州    1
西安    2
太原    3
Name: 区域, dtype: int64


# 如果想得出计数占比，可以加参数 normalize=True：
In [5]: df['区域'].value_counts(normalize=True)
Out[5]:
太原    0.500000
西安    0.333333
郑州    0.166667
Name: 区域, dtype: float64
```

## **DataFrame 情况**

```python
In [6]: df = pd.DataFrame({'区域1' : ['西安', '太原', '西安', '太原', '郑州', '太原'],^M
   ...:                    '区域2' : ['太原', '太原', '西安', '西安', '西安', '太原']})

In [7]: df.apply(pd.value_counts)
Out[7]:
    区域1  区域2
太原    3  3.0
西安    2  3.0
郑州    1  NaN
# 区域2中没有郑州，所以是NaN。
```

## 属性 `index`

```python
In [1]: import pandas as pd^M
   ...: df = pd.DataFrame({'区域' : ['西安', '太原', '西安', '太原', '郑州', '太原'], ^M
   ...:                   '10月份销售' : ['0.477468', '0.195046', '0.015964', '0.259654', '0.856412', '0.259644'],^M
   ...:                   '9月份销售' : ['0.347705', '0.151220', '0.895599', '0236547', '0.569841', '0.254784']})

In [2]: df
Out[2]:
   区域    10月份销售     9月份销售
0  西安  0.477468  0.347705
1  太原  0.195046  0.151220
2  西安  0.015964  0.895599
3  太原  0.259654   0236547
4  郑州  0.856412  0.569841
5  太原  0.259644  0.254784

In [3]: df['区域'].value_counts()
Out[3]:
太原    3
西安    2
郑州    1
Name: 区域, dtype: int64

In [4]: df['区域'].value_counts().index
Out[4]: Index(['太原', '西安', '郑州'], dtype='object')
```

## 属性 `values`

```python
In [5]: df['区域'].value_counts().values
Out[5]: array([3, 2, 1], dtype=int64)
```

参考

<a href="https://www.cnblogs.com/keye/p/9664414.html" blank="">pandas计数 value_counts()</a>  