# Numpy mgrid()和meshgrid()的区别和使用

## **mgrid**

用法：返回多维结构，常见的如2D图形，3D图形。对比np.meshgrid，在处理大数据时速度更快，且能处理多维（np.meshgrid只能处理2维）
ret = np.mgrid[ 第1维，第2维 ，第3维 ， …]

**返回多值，以多个矩阵的形式返回，第1返回值为第1维数据在最终结构中的分布，第2返回值为第2维数据在最终结构中的分布，以此类推**。（分布以矩阵形式呈现）

例如 `np.mgrid[X , Y]`
样本（i，j）的坐标为 （X[i，j] ,Y[i，j]）,X代表第1维，Y代表第2维，在此例中分别为横纵坐标。



**`mgrid[[1:3:3j, 4:5:2j]]`** 
3j：3个点

- - **步长为复数表示点数，左闭右闭**
  - **步长为实数表示间隔，左闭右开**





例如1D结构（array），如下：

```python
In [2]: import numpy as np

In [3]: pp=np.mgrid[-5:5:5j]

In [4]: pp
Out[4]: array([-5. , -2.5,  0. ,  2.5,  5. ])
```

例如2D结构 (2D矩阵)，如下：

```python
>>> pp = np.mgrid[-1:1:2j,-2:2:3j]
>>> x , y = pp
>>> x
array([[-1., -1., -1.],
       [ 1.,  1.,  1.]])
>>> y 
array([[-2.,  0.,  2.],
       [-2.,  0.,  2.]])
```

例如3D结构 (3D立方体)，如下：

```python
>>> pp = np.mgrid[-1:1:2j,-2:2:3j,-3:3:5j]
>>> print pp
[[[[-1.  -1.  -1.  -1.  -1. ]
   [-1.  -1.  -1.  -1.  -1. ]
   [-1.  -1.  -1.  -1.  -1. ]]

  [[ 1.   1.   1.   1.   1. ]
   [ 1.   1.   1.   1.   1. ]
   [ 1.   1.   1.   1.   1. ]]]


 [[[-2.  -2.  -2.  -2.  -2. ]
   [ 0.   0.   0.   0.   0. ]
   [ 2.   2.   2.   2.   2. ]]

  [[-2.  -2.  -2.  -2.  -2. ]
   [ 0.   0.   0.   0.   0. ]
   [ 2.   2.   2.   2.   2. ]]]


 [[[-3.  -1.5  0.   1.5  3. ]
   [-3.  -1.5  0.   1.5  3. ]
   [-3.  -1.5  0.   1.5  3. ]]

  [[-3.  -1.5  0.   1.5  3. ]
   [-3.  -1.5  0.   1.5  3. ]
   [-3.  -1.5  0.   1.5  3. ]]]]
```

## **meshgrid**

meshgrid函数通常使用在数据的矢量化上。

它适用于生成网格型数据，可以接受两个一维数组生成两个二维矩阵，对应两个数组中所有的 (x,y) 对。

```python
In [4]: import numpy as np

In [5]: xnums = np.arange(4)

In [6]: ynums = np.arange(5)

In [7]: xnums
Out[7]: array([0, 1, 2, 3])

In [8]: ynums
Out[8]: array([0, 1, 2, 3, 4])

In [9]: data_list = np.meshgrid(xnums, ynums)

In [10]: data_list
Out[10]:
[array([[0, 1, 2, 3],
        [0, 1, 2, 3],
        [0, 1, 2, 3],
        [0, 1, 2, 3],
        [0, 1, 2, 3]]), array([[0, 0, 0, 0],
        [1, 1, 1, 1],
        [2, 2, 2, 2],
        [3, 3, 3, 3],
        [4, 4, 4, 4]])]

In [11]: x, y = data_list

In [12]: x.shape
Out[12]: (5, 4)

In [13]: y.shape
Out[13]: (5, 4)

In [14]: x
Out[14]:
array([[0, 1, 2, 3],
       [0, 1, 2, 3],
       [0, 1, 2, 3],
       [0, 1, 2, 3],
       [0, 1, 2, 3]])

In [15]: y
Out[15]:
array([[0, 0, 0, 0],
       [1, 1, 1, 1],
       [2, 2, 2, 2],
       [3, 3, 3, 3],
       [4, 4, 4, 4]])
```

meshgrid的**作用**是：

**根据传入的两个一维数组参数生成两个数组元素的列表。**

如果

第一个参数是 xarray，维度是 xdimesion，

第二个参数是 yarray，维度是y dimesion。

那么生成的第一个二维数组是以xarray为行，共 ydimesion 行的向量；

而第二个二维数组是以 yarray 的转置为列，共 xdimesion 列的向量。

## **meshgrid 和 mgrid 的区别**

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200508101111.png"/>



参考

<a href="https://www.cnblogs.com/shenxiaolin/p/8854197.html" blank="">Python的 numpy中 meshgrid 和 mgrid 的区别和使用</a> 

