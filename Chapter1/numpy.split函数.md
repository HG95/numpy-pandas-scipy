# numpy.split()函数

```python
np.split(ary, indices_or_sections, axis=0)
```

函数功能：

把一个数组从左到右按顺序切分

参数：

- `ary`：要切分的数组

- `indices_or_sections`：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置

- `axis`：沿着哪个维度进行切向，默认为0，横向切分

**一维数组**

```python
x = np.array([0,1,2,3,4,5,6,7,8])
print (np.split(x,3))
# [array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]
```

```python
print (np.split(x,[3,5,6,9]))
# [array([0, 1, 2]), array([3, 4]), array([5]), array([6, 7, 8]),
# array([], dtype=int32)]

```

```python
print(np.split(x,[3,5,6,8]))

# [array([0, 1, 2]), array([3, 4]), array([5]), array([6, 7]), array([8])]
```

当 `indices_or_sections` 为数组时，为`[)` 的情况：

很明显，因为一维数组只有一个维度，所以切分只会在这一个维度进行。第一行输出对应indices_or_sections参数为一个整数，将数组平均分成了三份，第二行输出对应indices_or_sections参数为一个数组，此时每一次切分都会将要切分数组的前n（n=3,5，6,9）个元素切分出来，第一次n=3，进行数组切分得到array([0, 1, 2])，第二次n=5，进行数组切分得到array([3, 4])，此时数组前5个元素已经切分完毕，后续同理，最后一次n=9，切分完毕后数组所有元素已经被切分，所以最后一个array为array([], dtype=int32)，对比第三行输出可以看出区别。

**二维数组**

```python
import numpy as np

a = np.array([[1,2,3],
     [1,2,5],
     [4,6,7]])
print (np.split(a, [2, 3],axis = 0))

[array([[1, 2, 3],
       [1, 2, 5]]), array([[4, 6, 7]]), array([], shape=(0, 3), dtype=int32)]



print (np.split(a, [1, 2],axis = 1))
[array([[1],
       [1],
       [4]]), array([[2],
       [2],
       [6]]), array([[3],
       [5],
       [7]])]
```

