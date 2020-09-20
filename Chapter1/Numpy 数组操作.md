# Numpy 数组操作

## 连接数组

### `np.c_`和 `np.r_`

- `np.r_`是按列连接两个矩阵，就 是把两矩阵上下相加，要求列数相等，类似于pandas中的concat()。
- `np.c_`是按行连接两个矩阵，就是把两矩阵左右相加，要求行数相等，类似于pandas中的merge()。

```python
import numpy as np
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

np.c_[a,b]
array([[1, 4],
       [2, 5],
       [3, 6]])
       
np.r_[a,b]
array([1, 2, 3, 4, 5, 6])

```



### `numpy.concatenate`

`numpy.concatenate` 函数用于沿指定轴连接相同形状的两个或多个数组，格式如下：
`numpy.concatenate((a1, a2, ...), axis)`

**数说明：**

- a1, a2, …：相同类型的数组
- axis：沿着它连接数组的轴，默认为 0

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
# 两个数组的维度相同
 
print ('沿轴 0 连接两个数组：')
print (np.concatenate((a,b)))
print ('\n')
 
print ('沿轴 1 连接两个数组：')
print (np.concatenate((a,b),axis = 1))

第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


沿轴 0 连接两个数组：
[[1 2]
 [3 4]
 [5 6]
 [7 8]]


沿轴 1 连接两个数组：
[[1 2 5 6]
 [3 4 7 8]]


```

### `numpy.stack`

`numpy.stack `函数用于沿新轴连接数组序列，格式如下：
`numpy.stack(arrays, axis)`
参数说明：

- arrays相同形状的数组序列
- axis：返回数组中的轴，输入数组沿着它来堆叠

```python

import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
 
print ('沿轴 0 堆叠两个数组：')
print (np.stack((a,b),0))
print ('\n')
 
print ('沿轴 1 堆叠两个数组：')
print (np.stack((a,b),1))

第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


沿轴 0 堆叠两个数组：
[[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]


沿轴 1 堆叠两个数组：
[[[1 2]
  [5 6]]

 [[3 4]
  [7 8]]]

```

### `numpy.hstack`

`numpy.hstack` 是 `numpy.stack` 函数的变体，它通过水平堆叠来生成数组。

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
 
print ('水平堆叠：')
c = np.hstack((a,b))
print (c)
print ('\n')

第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


水平堆叠：
[[1 2 5 6]
 [3 4 7 8]]

```

### `numpy.vstack`

`numpy.vstack `是`numpy.stack `函数的变体，它通过垂直堆叠来生成数组。

```python
import numpy as np
 
a = np.array([[1,2],[3,4]])
 
print ('第一个数组：')
print (a)
print ('\n')
b = np.array([[5,6],[7,8]])
 
print ('第二个数组：')
print (b)
print ('\n')
 
print ('竖直堆叠：')
c = np.vstack((a,b))
print (c)
第一个数组：
[[1 2]
 [3 4]]


第二个数组：
[[5 6]
 [7 8]]


竖直堆叠：
[[1 2]
 [3 4]
 [5 6]
 [7 8]]

```

## 分割数组

### `numpy.split`

`numpy.split `函数沿特定的轴将数组分割为子数组，格式如下：
`numpy.split(ary, indices_or_sections, axis)`

**数说明：**

- ary：被分割的数组
- indices_or_sections：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭）
- axis：沿着哪个维度进行切向，默认为0，横向切分。为1时，纵向切分

```python
import numpy as np
 
a = np.arange(9)
 
print ('第一个数组：')
print (a)
print ('\n')
 
print ('将数组分为三个大小相等的子数组：')
b = np.split(a,3)
print (b)
print ('\n')
 
print ('将数组在一维数组中表明的位置分割：')
b = np.split(a,[4,7])
print (b)
第一个数组：
[0 1 2 3 4 5 6 7 8]


将数组分为三个大小相等的子数组：
[array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]


将数组在一维数组中表明的位置分割：
[array([0, 1, 2, 3]), array([4, 5, 6]), array([7, 8])]

```

### `numpy.hsplit`

`numpy.hsplit` 函数用于水平分割数组，通过指定要返回的相同形状的数组数量来拆分原数组。

```python
import numpy as np
 
harr = np.floor(10 * np.random.random((2, 6)))
print ('原array：')
print(harr)
 
print ('拆分后：')
print(np.hsplit(harr, 3))

原array：
[[4. 7. 6. 3. 2. 6.]
 [6. 3. 6. 7. 9. 7.]]
拆分后：
[array([[4., 7.],
       [6., 3.]]), array([[6., 3.],
       [6., 7.]]), array([[2., 6.],
       [9., 7.]])]


```

### `numpy.vsplit`

`numpy.vsplit `沿着垂直轴分割，其分割方式与hsplit用法相同。

```python
import numpy as np
 
a = np.arange(16).reshape(4,4)
 
print ('第一个数组：')
print (a)
print ('\n')
 
print ('竖直分割：')
b = np.vsplit(a,2)
print (b)


第一个数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]


竖直分割：
[array([[0, 1, 2, 3],
       [4, 5, 6, 7]]), array([[ 8,  9, 10, 11],
       [12, 13, 14, 15]])]


```

## 数组元素的添加

### `numpy.resize`

`numpy.resize` 函数返回指定大小的新数组。
如果新数组大小大于原始大小，则包含原始数组中的元素的副本。

`numpy.resize(arr, shape)`
**参数说明：**

- arr：要修改大小的数组
- shape：返回数组的新形状

```python
import numpy as np
 
a = np.array([[1,2,3],[4,5,6]])
 
print ('第一个数组：')
print (a)
第一个数组：
[[1 2 3]
 [4 5 6]]
print ('\n')
 
print ('第一个数组的形状：')
print (a.shape)
第一个数组的形状：
(2, 3)
print ('\n')
b = np.resize(a, (3,2))
 
print ('第二个数组：')
print (b)
第二个数组：
[[1 2]
 [3 4]
 [5 6]]
print ('\n')
 
print ('第二个数组的形状：')
print (b.shape)
第二个数组的形状：
(3, 2)
print ('\n')
# 要注意 a 的第一行在 b 中重复出现，因为尺寸变大了
 
print ('修改第二个数组的大小：')
b = np.resize(a,(3,3))
print (b)
修改第二个数组的大小：
[[1 2 3]
 [4 5 6]
 [1 2 3]]

```

### `numpy.append`

`numpy.append `函数在数组的末尾添加值。 追加操作会分配整个数组，并把原来的数组复制到新数组中。 此外，输入数组的维度必须匹配否则将生成ValueError。

append 函数返回的始终是一个一维数组。
`numpy.append(arr, values, axis=None)`
参数说明：

- arr：输入数组
- values：要向arr添加的值，需要和arr形状相同（除了要添加的轴）
- axis：默认为 None。当axis无定义时，是横向加成，返回总是为一维数组！当axis有定义的时候，分别为0和1的时候。当axis有定义的时候，分别为0和1的时候（列数要相同）。当axis为1时，数组是加在右边（行数要相同）。
  

### `numpy.insert`

`numpy.insert `函数在给定索引之前，沿给定轴在输入数组中插入值。

如果值的类型转换为要插入，则它与输入数组不同。 插入没有原地的，函数会返回一个新数组。 此外，如果未提供轴，则输入数组会被展开。
`numpy.insert(arr, obj, values, axis)`

**参数说明：**

- arr：输入数组
- obj：在其之前插入值的索引
- values：要插入的值
- axis：沿着它插入的轴，如果未提供，则输入数组会被展开

```python
import numpy as np
 
a = np.array([[1,2],[3,4],[5,6]])
 
print ('第一个数组：')
print (a)
第一个数组：
[[1 2]
 [3 4]
 [5 6]]
print ('\n')
 
print ('未传递 Axis 参数。 在插入之前输入数组会被展开。')
print (np.insert(a,3,[11,12]))
未传递 Axis 参数。 在插入之前输入数组会被展开。
[ 1  2  3 11 12  4  5  6]
print ('\n')
print ('传递了 Axis 参数。 会广播值数组来配输入数组。')
 
print ('沿轴 0 广播：')
print (np.insert(a,1,[11],axis = 0))

传递了 Axis 参数。 会广播值数组来配输入数组。
沿轴 0 广播：
[[ 1  2]
 [11 11]
 [ 3  4]
 [ 5  6]]
print ('\n')
 
print ('沿轴 1 广播：')
print (np.insert(a,1,11,axis = 1))
沿轴 1 广播：
[[ 1 11  2]
 [ 3 11  4]
 [ 5 11  6]]

```

### `numpy.unique`

`numpy.unique `函数用于去除数组中的重复元素。

`numpy.unique` 函数用于去除数组中的重复元素。
`numpy.unique(arr, return_index, return_inverse, return_counts)`

- arr：输入数组，如果不是一维数组则会展开
- `return_index`：如果为true，返回新列表元素在旧列表中的位置（下标），并以列表形式储
- `return_inverse`：如果为true，返回旧列表元素在新列表中的位置（下标），并以列表形式储
- `return_counts`：如果为true，返回去重数组中的元素在原数组中的出现次数


```python
import numpy as np
 
a = np.array([5,2,6,2,7,5,6,8,2,9])
 
print ('第一个数组：')
print (a)
第一个数组：
[5 2 6 2 7 5 6 8 2 9]
print ('\n')
 
print ('第一个数组的去重值：')
u = np.unique(a)
print (u)
第一个数组的去重值：
[2 5 6 7 8 9]
print ('\n')
 
print ('去重数组的索引数组：')
# 返回值为两个
u,indices = np.unique(a, return_index = True)
print (indices)
去重数组在原数组中的索引，构成的数组：
[1 0 2 4 7 9]
print ('\n')
 
print ('我们可以看到每个和原数组下标对应的数值：')
print (a)
我们可以看到每个和原数组下标对应的数值：
[5 2 6 2 7 5 6 8 2 9]
print ('\n')
 
print ('去重数组的下标：')
# 返回值为两个   indices 旧数组中的元素在去重后的数组中的索引，构成的数组
u,indices = np.unique(a,return_inverse = True)
print (u)
去重数组的下标：
[2 5 6 7 8 9]
print ('\n')
 
print ('下标为：')
print (indices)
下标为：
[1 0 2 0 3 1 2 4 0 5]
print ('\n')
 
print ('使用下标重构原数组：')
print (u[indices])
使用下标重构原数组：
[5 2 6 2 7 5 6 8 2 9]
print ('\n')
 
print ('返回去重元素的重复数量：')
#u去重后的数组，indices 去重后的数组中的元素在原来数组中出现的次数
u,indices = np.unique(a,return_counts = True)
print (u)
print (indices)
返回去重元素的重复数量：
[2 5 6 7 8 9]
[3 2 2 1 1 1]
```

### `numpy.delete`

numpy.delete 函数返回从输入数组中删除指定子数组的新数组。 与 insert() 函数的情况一样，如果未提供轴参数，则输入数组将展开。
`Numpy.delete(arr, obj, axis)`

**参数说明：**

- arr：输入数组
- obj：可以被切片，整数或者整数数组，表明要从输入数组删除的子数组
- axis：沿着它删除给定子数组的轴，如果未提供，则输入数组会被展开

```python
import numpy as np
 
a = np.arange(12).reshape(3,4)
 
print ('第一个数组：')
print (a)
第一个数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
print ('\n')
 
print ('未传递 Axis 参数。 在插入之前输入数组会被展开。')
print (np.delete(a,5))
未传递 Axis 参数。 在插入之前输入数组会被展开。
[ 0  1  2  3  4  6  7  8  9 10 11]
print ('\n')
 
print ('删除第二列：')
print (np.delete(a,1,axis = 1))
未传递 Axis 参数。 在插入之前输入数组会被展开。
[ 0  1  2  3  4  6  7  8  9 10 11]
print ('\n')
 
print ('包含从数组中删除的替代值的切片：')
a = np.array([1,2,3,4,5,6,7,8,9,10])
print (np.delete(a, np.s_[::2]))
包含从数组中删除的替代值的切片：
[ 2  4  6  8 10]

```

