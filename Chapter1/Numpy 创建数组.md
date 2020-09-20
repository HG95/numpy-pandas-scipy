# Numpy 创建数组

## `numpy.empty`

`numpy.empty`方法用来创建一个指定 形状（shape）、数据类型（dtype）且未初始化的数组：
`numpy.empty(shape, dtype = float, order = 'C')`

- **hape**：int或tuple

> 空数组的形状

- **dtype**：数据类型，可选

> 所需的输出数据类型。

- **order**：{'C'，'F'}，可选

> 是否在存储器中以行主（C风格）或列主（Fortran风格）顺序存储多维数据。

返回

给定形状，dtype和顺序的未初始化（任意）数据的数组。对象数组将初始化为无。

```python
#创建三行两列的数组
import numpy as np 
x = np.empty([3,2], dtype = int) 
print (x)

# 注意 − 数组元素为随机值，因为它们未初始化。
#[[ 6917529027641081856  5764616291768666155]
# [ 6917529027641081859 -5764598754299804209]
# [          4497473538      844429428932120]]


```

## `numpy.zeros`

创建指定大小的数组，数组元素以 0 来填充：
`numpy.zeros(shape, dtype = float, order = 'C')`

**shape**：int或ints序列

> 新数组的形状，例如`（2， 3）`或`2`。

**dtype**：数据类型，可选

> 数组的所需数据类型，例如`numpy.int8`。默认值为`numpy.float64`。

**order**：{'C'，'F'}，可选

> 是否在存储器中以C或Fortran连续（按行或列方式）存储多维数据。

```python
import numpy as np
 
# 默认为浮点数
x = np.zeros(5) 
print(x)
# [0. 0. 0. 0. 0.]
 
# 设置类型为整数
y = np.zeros((5,), dtype = np.int) 
print(y)
# [0 0 0 0 0]

# 自定义类型
z = np.zeros((2,2), dtype = [('x', 'i4'), ('y', 'i4')])  
print(z)
#[[(0, 0) (0, 0)]
# [(0, 0) (0, 0)]]

```

## `numpy.ones`

创建指定形状的数组，数组元素以 1 来填充：
`numpy.ones(shape, dtype = None, order = 'C')`

**shape**：int或ints序列

> 新数组的形状，例如`（2， 3）`或`2`。

**dtype**：数据类型，可选

> 数组的所需数据类型，例如`numpy.int8`。默认值为`numpy.float64`。

**order**：{'C'，'F'}，可选

> 是否在存储器中以C或Fortran连续（按行或列方式）存储多维数据。

```python
import numpy as np
 
# 默认为浮点数
x = np.ones(5) 
print(x)
 # [1. 1. 1. 1. 1.]
# 自定义类型
x = np.ones([2,2], dtype = int)
print(x)
#[[1 1]
# [1 1]]

```

## Numerical ranges

### `numpy.arange()`

`numpy.arange([start,]stop,[step,]dtype=None)`

在给定间隔内返回均匀间隔的值。

在半开区间`[开始， 停止）`（换句话说，包括*开始 t3 >但不包括\*停止\*）。*对于整数参数，该函数等效于Python内置的[range](http://docs.python.org/lib/built-in-funcs.html)函数，但返回一个ndarray而不是一个列表。

```python
>>> np.arange(3)
array([0, 1, 2])
>>> np.arange(3.0)
array([ 0.,  1.,  2.])
>>> np.arange(3,7)
array([3, 4, 5, 6])
>>> np.arange(3,7,2)
array([3, 5])
```

### `numpy.linspace()`

`numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)`

在指定的间隔内返回均匀间隔的数字。

返回num均匀分布的样本，在 [start, stop]。

这个区间的端点可以任意的被排除在外。

参数：

- start : scalar(标量)   序列的起始值

- stop : scala    序列的结束点，除非endpoint被设置为False，在这种情况下, the sequence consists of all but the last of num + 1 evenly spaced samples(该序列包括所有除了最后的num+1上均匀分布的样本(感觉这样翻译有点坑)), 以致于stop被排除.当endpoint is False的时候注意步长的大小(下面有例子).

- num : int, optional(可选) 生成的样本数，默认是50。必须是非负。

- endpoint : bool, optional
  如果是真，则一定包括stop，如果为False，一定不会有stop

- retstep : bool, optional  如果为真，返回（*样本*，*步骤*），其中*步长*是样本之间的间距。

- dtype : dtype, optional

返回：

- **samples**：ndarray

- **step **：float

  > 仅在*retstep*为True时返回
  >
  > 样本之间的间距大小。

```python
>>> np.linspace(2.0, 3.0, num=5)
    array([ 2.  ,  2.25,  2.5 ,  2.75,  3.  ])
>>> np.linspace(2.0, 3.0, num=5, endpoint=False)
    array([ 2. ,  2.2,  2.4,  2.6,  2.8])
>>> np.linspace(2.0, 3.0, num=5, retstep=True)
    (array([ 2.  ,  2.25,  2.5 ,  2.75,  3.  ]), 0.25)
```

## Building matrices

### `numpy.diag()`

提取对角线或构造对角数组。

`numpy.diag(v,k=0)`

- v 是一个**1维数组**时，结果形成一个以一维数组为对角线元素的矩阵

- v 是一个**二维矩阵**时，结果输出矩阵的对角线元素

- `k` : int, optional  对角线的位置，大于零位于对角线上面，小于零则在下面。

```python
>>> x = np.arange(9).reshape((3,3))
>>> x
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])
       
>>> np.diag(x)
array([0, 4, 8])
>>> np.diag(x, k=1)
array([1, 5])
>>> np.diag(x, k=-1)
array([3, 7])

>>> np.diag(np.diag(x))
array([[0, 0, 0],
       [0, 4, 0],
       [0, 0, 8]])

```

