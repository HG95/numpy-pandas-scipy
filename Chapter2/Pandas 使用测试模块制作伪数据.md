# Pandas 使用测试模块制作伪数据

在pandas中，有一个测试模块可以帮助我们生成半真实（伪数据），并进行测试，它就是**util.testing**。


## 创建随机数据集
```python
df = pd.util.testing.makeDataFrame()
```



## 创建随机日期索引数据集
```python
df = pd.util.testing.makePeriodFrame()
df = pd.util.testing.makeTimeDataFrame()
```



## 创建随机混合类型数据集
```python
df = pd.util.testing.makeMixedDataFrame()
```

```python
>>> import pandas.util.testing as tm
>>> tm.N, tm.K = 15, 3  # 默认的行和列

>>> import numpy as np
>>> np.random.seed(444)

>>> tm.makeTimeDataFrame(freq='M').head()
                 A       B       C
2000-01-31  0.3574 -0.8804  0.2669
2000-02-29  0.3775  0.1526 -0.4803
2000-03-31  1.3823  0.2503  0.3008
2000-04-30  1.1755  0.0785 -0.1791
2000-05-31 -0.9393 -0.9039  1.1837

>>> tm.makeDataFrame().head()
                 A       B       C
nTLGGTiRHF -0.6228  0.6459  0.1251
WPBRn9jtsR -0.3187 -0.8091  1.1501
7B3wWfvuDA -1.9872 -1.0795  0.2987
yJ0BTjehH1  0.8802  0.7403 -1.2154
0luaYUYvy1 -0.9320  1.2912 -0.2907
```

## 创建随机个数的字符串

```python
pd.util.testing.rands(n)
```

```python
[pd.util.testing.rands(3) for _ in range(4)]
# ['crx', 'Z9k', 'KAU', 'mHz']
```

`pd.util.testing.rand(n)`

随机创建含有三个元素的数组

```python
[pd.util.testing.rand(3) for _ in range(4)]

[array([0.72753901, 0.01316105, 0.12749649]),
 array([0.68111966, 0.30113528, 0.27567208]),
 array([0.55361183, 0.19179808, 0.89546358]),
 array([0.97648769, 0.94504658, 0.1353476 ])]
```

`pd.util.testing.rands_array(nchars, size, dtype='O')`

创建字符串矩阵

```
[pd.util.testing.rands_array(2,size=(2,2)) for _ in range(4)]


[array([['YX', 'u9'],
        ['MY', 'Fa']], dtype=object), 
 array([['Fa', 'CQ'],
        ['Kf', 'IR']], dtype=object), 
 array([['Lz', 'q8'],
        ['1S', 'WU']], dtype=object), 
 array([['EC', 'Jz'],
        ['2z', '6g']], dtype=object)]

```



`pd.util.testing.randbool(iterable)`

根据 iterable 的shape 创建 boolen 类型的 iterable

```python
[pd.util.testing.randbool([1,2]) for _ in range(4)]

[array([[ True,  True]]),
 array([[False, False]]),
 array([[ True, False]]),
 array([[ True,  True]])]
```

