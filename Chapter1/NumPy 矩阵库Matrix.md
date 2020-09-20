# NumPy 矩阵库(Matrix)

NumPy 中包含了一个矩阵库 numpy.matlib，该模块中的函数返回的是一个矩阵，而不是 ndarray 对象。
一个m*n 的矩阵是一个由行（mrow）列n（column）元素排列成的矩形阵列。

矩阵里的元素可以是数字、符号或数学式。以下是一个由 6 个数字元素构成的 2 行 3 列的矩阵：


## `matlib.empty()`

matlib.empty() 函数返回一个新的矩阵，语法格式为：
`numpy.matlib.empty(shape, dtype, order)`

返回给定形状和类型的新矩阵，而不初始化条目。

参数说明：

- shape: 定义新矩阵形状的整数或整数元组
- Dtype: 可选，数据类型
- order: C（行序优先） 或者 F（列序优先）

```python
>>> import numpy.matlib
>>> np.matlib.empty((2, 2))    # filled with random data
matrix([[  6.76425276e-320,   9.79033856e-307],
        [  7.39337286e-309,   3.22135945e-309]])        #random
>>> np.matlib.empty((2, 2), dtype=int)
matrix([[ 6600475,        0],
        [ 6586976, 22740995]])                          #random
```

## `numpy.matlib.zeros()`

numpy.matlib.zeros() 函数创建一个以 0 填充的矩阵。

- `shape`**：int或ints序列矩阵的形状**

- `dtype`**：数据类型，可选矩阵的所需数据类型，默认为float。**
- `order`：{'C'，'F'}，可选是否以C或Fortran连续顺序存储结果，默认值为“C”。

如果`shape`具有长度一即`(N,)`或者是标量`N`，则*out*形状矩阵`(1,N)`。

```python
>>> import numpy.matlib
>>> np.matlib.zeros((2, 3))
matrix([[ 0.,  0.,  0.],
        [ 0.,  0.,  0.]])
>>> np.matlib.zeros(2)
matrix([[ 0.,  0.]])
```

## `numpy.matlib.ones()`

矩阵的一。

返回给定形状和类型的矩阵，用一个填充。

- **shape**：{sequence of ints，int} 矩阵的形状

- **dtype**：数据类型，可选 矩阵的所需数据类型，默认为np.float64。

- **order**：{'C'，'F'}，可选是否以C或Fortran连续顺序存储矩阵，默认值为“C”。

```python
>>> np.matlib.ones((2,3))
matrix([[ 1.,  1.,  1.],
        [ 1.,  1.,  1.]])
>>> np.matlib.ones(2)
matrix([[ 1.,  1.]])
```

## `numpy.matlib.eye()`

numpy.matlib.eye() 函数返回一个矩阵，对角线元素为 1，其他位置为零。

`numpy.matlib.eye(n, M,k, dtype)`
参数说明：

- n: 返回矩阵的行数
- M: 返回矩阵的列数，默认为 n
- k: 对角线的索引 , 0表示主对角线，正值表示上对角线，负值表示下对角线。
- dtype: 数据类型

```python
>>> import numpy.matlib
>>> np.matlib.eye(3, k=1, dtype=float)
matrix([[ 0.,  1.,  0.],
        [ 0.,  0.,  1.],
        [ 0.,  0.,  0.]])
```

[`numpy.eye`](http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.eye.html#numpy.eye) 等效数组功能。

## `numpy.matlib.identity()`

`numpy.matlib.identity(n,dtype=None) `函数返回给定大小的单位矩阵。

单位矩阵是个方阵，从左上角到右下角的对角线（称为主对角线）上的元素均为 1，除此以外全都为 0。

- **n**：int 返回的单位矩阵的大小。

- **dtype**：数据类型，可选  输出的数据类型。默认为`float`。

```python
>>> import numpy.matlib
>>> np.matlib.identity(3, dtype=int)
matrix([[1, 0, 0],
        [0, 1, 0],
        [0, 0, 1]])
```

[`numpy.identity`](http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.identity.html#numpy.identity) 等效数组功能。

## `numpy.matlib.rand()`

`numpy.matlib.rand(*args) `函数创建一个给定大小的矩阵，数据是随机填充的。

返回具有给定形状的随机值矩阵。

创建给定形状的矩阵，并通过`[0， 1）`的均匀分布的随机样本传播它。

*** args**：参数

输出形状。如果给定为N个整数，每个整数指定一个维度的大小。如果给出一个元组，这个元组给出完整的形状。

```python
>>> import numpy.matlib
>>> np.matlib.rand(2, 3)
matrix([[ 0.68340382,  0.67926887,  0.83271405],
        [ 0.00793551,  0.20468222,  0.95253525]])       #random
>>> np.matlib.rand((2, 3))
matrix([[ 0.84682055,  0.73626594,  0.11308016],
        [ 0.85429008,  0.3294825 ,  0.89139555]])       #random
如果第一个参数是元组，则忽略其他参数：

>>> np.matlib.rand((2, 3), 4)
matrix([[ 0.46898646,  0.15163588,  0.95188261],
        [ 0.59208621,  0.09561818,  0.00583606]])       #random
```

## `nump.mat()`

将输入解释为矩阵。

`numpy.mat(data, dtype=None)`

- **data**：array_like 输入数据。

- **dtype**：数据类型  输出矩阵的数据类型。

```python
>>> from numpy import *
>>> a1=array([1,2,3])
>>> a1
array([1, 2, 3])
>>> a1=mat(a1)
>>> a1
matrix([[1, 2, 3]])
>>> shape(a1)
(1, 3)
>>> b=matrix([1,2,3])
>>> shape(b)
(1, 3)
```

## 创建常见的矩阵

```python
>>>data1=mat(zeros((3,3))) #创建一个3*3的零矩阵，矩阵这里zeros函数的参数是一个tuple类型(3,3)
>>> data1
matrix([[ 0.,  0.,  0.],
        [ 0.,  0.,  0.],
        [ 0.,  0.,  0.]])
>>>data2=mat(ones((2,4))) #创建一个2*4的1矩阵，默认是浮点型的数据，如果需要时int类型，可以使用dtype=int
>>> data2
matrix([[ 1.,  1.,  1.,  1.],
        [ 1.,  1.,  1.,  1.]])
>>>data3=mat(random.rand(2,2)) #这里的random模块使用的是numpy中的random模块，random.rand(2,2)创建的是一个二维数组，需要将其转换成#matrix
>>> data3
matrix([[ 0.57341802,  0.51016034],
        [ 0.56438599,  0.70515605]])
>>>data4=mat(random.randint(10,size=(3,3))) #生成一个3*3的0-10之间的随机整数矩阵，如果需要指定下界则可以多加一个参数
>>> data4
matrix([[9, 5, 6],
        [3, 0, 4],
        [6, 0, 7]])
>>>data5=mat(random.randint(2,8,size=(2,5))) #产生一个2-8之间的随机整数矩阵
>>> data5
matrix([[5, 4, 6, 3, 7],
        [5, 3, 3, 4, 6]])
>>>data6=mat(eye(2,2,dtype=int)) #产生一个2*2的对角矩阵
>>> data6
matrix([[1, 0],
        [0, 1]])
 
a1=[1,2,3]
a2=mat(diag(a1)) #生成一个对角线为1、2、3的对角矩阵
>>> a2
matrix([[1, 0, 0],
        [0, 2, 0],
        [0, 0, 3]])
```

## 矩阵运算

### 矩阵相乘

```python
a1=mat([1,2]);      
a2=mat([[1],[2]]);
a3=a1*a2;
#1*2的矩阵乘以2*1的矩阵，得到1*1的矩阵

```

### 矩阵点乘(矩阵对应元素相乘)

矩阵对应元素相乘

```python
a1=mat([3,1])
a2=mat([2,2])
a3=multiply(a1,a2)
# matrix([[6, 2]])
```



### 矩阵求逆，转置

矩阵求逆

```python
>>>a1=mat(eye(2,2)*0.5)
>>> a1
matrix([[ 0.5,  0. ],
        [ 0. ,  0.5]])
>>>a2=a1.I  #求矩阵matrix([[0.5,0],[0,0.5]])的逆矩阵
>>> a2
matrix([[ 2.,  0.],
        [ 0.,  2.]])

```

矩阵转置

```python
>>> a1=mat([[1,1],[0,0]])
>>> a1
matrix([[1, 1],
        [0, 0]])
>>> a2=a1.T
>>> a2
matrix([[1, 0],
        [1, 0]])

```

### 矩阵的分隔和合并

矩阵的分隔，同列表和数组的分隔一致。

```python
>>>a=mat(ones((3,3)))
>>> a
matrix([[ 1.,  1.,  1.],
        [ 1.,  1.,  1.],
        [ 1.,  1.,  1.]])
>>>b=a[1:,1:]  #分割出第二行以后的行和第二列以后的列的所有元素
>>> b
matrix([[ 1.,  1.],
        [ 1.,  1.]])

```

**矩阵的合并**

```python
>>>a=mat(ones((2,2)))
>>> a
matrix([[ 1.,  1.],
        [ 1.,  1.]])
>>>b=mat(eye(2))
>>> b
matrix([[ 1.,  0.],
        [ 0.,  1.]])
>>>c=vstack((a,b))  #按列合并，即增加行数
>>> c
matrix([[ 1.,  1.],
        [ 1.,  1.],
        [ 1.,  0.],
        [ 0.,  1.]])
>>>d=hstack((a,b))  #按行合并，即行数不变，扩展列数
>>> d
matrix([[ 1.,  1.,  1.,  0.],
        [ 1.,  1.,  0.,  1.]])

```

## 扩展矩阵函数tile()

`tile(inX, (i,j))` ;i是扩展个数，j是扩展长度

```python
>>>x=mat([0,0,0])
>>> x
matrix([[0, 0, 0]])
>>> tile(x,(3,1))           #即将x扩展3个，j=1,表示其列数不变
matrix([[0, 0, 0],
        [0, 0, 0],
        [0, 0, 0]])
>>> tile(x,(2,2))           #x扩展2次，j=2,横向扩展
matrix([[0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0]])
```

