# Numpy 上三角矩阵triu和下三角矩阵tril

## numpy.tril

下三角矩阵

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200509151129.png"/>

```python
>>> np.tril([[1,2,3],[4,5,6],[7,8,9],[10,11,12]], -1)
array([[ 0,  0,  0],
       [ 4,  0,  0],
       [ 7,  8,  0],
       [10, 11, 12]])
```

## numpy.triu

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200509151234.png"/>

```
>>> np.triu([[1,2,3],[4,5,6],[7,8,9],[10,11,12]], -1)
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 0,  8,  9],
       [ 0,  0, 12]])
```

## numpy.triu_indices

```python
numpy.triu_indices(n, k=0, m=None)
```

参数：

- `n` : 返回的索引将有效的数组的大小。
- `k` : int 可选， 对角线偏移
- `m` : int 可选  返回的数组将有效的数组的列维度。默认情况下，*m*等于*n*。

返回

**inds**：元组，形状（2）的数组，形状（*n*）

> 三角形的索引。返回的元组包含两个数组，每个数组的索引沿着数组的一个维度。可用于切割形状的阵列（*n*，*n*）。

```python
In [29]: iu1 = np.triu_indices(3)

In [30]: iu2 = np.triu_indices(4)

In [31]: iu3 = np.triu_indices(4, 2)

In [32]: a = np.arange(16).reshape(4, 4)

In [33]: a
Out[33]:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])

In [34]: a[iu1]
Out[34]: array([ 0,  1,  2,  5,  6, 10])

In [35]: a[iu2]
Out[35]: array([ 0,  1,  2,  3,  5,  6,  7, 10, 11, 15])

In [36]: a[iu1]=-1

In [37]: a
Out[37]:
array([[-1, -1, -1,  3],
       [ 4, -1, -1,  7],
       [ 8,  9, -1, 11],
       [12, 13, 14, 15]])

In [38]: a[iu2] = -10

In [39]: a
Out[39]:
array([[-10, -10, -10, -10],
       [  4, -10, -10, -10],
       [  8,   9, -10, -10],
       [ 12,  13,  14, -10]])

In [40]: a = np.arange(16).reshape(4, 4)

In [41]: a
Out[41]:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])

In [42]: a[iu3]
Out[42]: array([2, 3, 7])

In [43]: a[iu3] = 100

In [44]: a
Out[44]:
array([[  0,   1, 100, 100],
       [  4,   5,   6, 100],
       [  8,   9,  10,  11],
       [ 12,  13,  14,  15]])
```

`numpy.tril_indices` 同理

## numpy.triu_indices_from

返回上三角矩阵的索引

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200509151931.png"/>

```python
data = np.random.randn(5,5)
mask = np.zeros_like(data)
mask
```

```
array([[0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.]])
```

```
np.triu_indices_from(mask)
```

```python
(array([0, 0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 3, 3, 4], dtype=int64),
 array([0, 1, 2, 3, 4, 1, 2, 3, 4, 2, 3, 4, 3, 4, 4], dtype=int64))
```

`numpy.tril_indices_from` 同理



参考：

<a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.triu.html#numpy.triu" blank="">官方文档</a> 

<a href="http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.triu_indices_from.html" blank="">官方文档(中)</a>  