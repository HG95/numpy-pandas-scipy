# NumPy 排序、条件刷选函数

NumPy 提供了多种排序的方法。 这些排序函数实现不同的排序算法，每个排序算法的特征在于执行速度，最坏情况性能，所需的工作空间和算法的稳定性。 下表显示了三种排序算法的比较。

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200428211613.png"/>

## `numpy.sort()`

`numpy.sort()` 函数返回输入数组的排序副本。函数格式如下：
参数说明：

- a: 要排序的数组
- axis: 沿着它排序数组的轴，如果没有数组会被展开，沿着最后的轴排序， axis=0 按列排序，axis=1 按行排序
- kind: 默认为’quicksort’（快速排序）
- order: 如果数组包含字段，则是要排序的字段

```python
import numpy as np

a = np.array([[3, 7], [9, 1]])
print(a)
# [[3 7]
#  [9 1]]
print('调用 sort() 函数：')
print(np.sort(a))
# [[3 7]
#  [1 9]]

print('按列排序：')
print(np.sort(a, axis=0))
# [[3 1]
#  [9 7]]

# 在 sort 函数中排序字段
dt = np.dtype([('name', 'S10'), ('age', int)])
a = np.array([("raju", 21), ("anil", 25), ("ravi", 17), ("amar", 27)], dtype=dt)
print('数组是：')
print(a)
#[(b'raju', 21) (b'anil', 25) (b'ravi', 17) (b'amar', 27)]

print('按 name 排序：')
print(np.sort(a, order='name'))
#[(b'amar', 27) (b'anil', 25) (b'raju', 21) (b'ravi', 17)]

```

`sorted()`

```python
sorted(iterable[, cmp[, key[, reverse]]])
sorted() 函数对所有可迭代的对象进行排序操作。
	sort 与 sorted 区别：
	sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。
	list 的 sort 方法返回的是对已经存在的列表进行操作，而内建函数 sorted 方法返回的是一个
	新的 list，而不是在原来的基础上进行的操作。
# sorted()可以利用参数reverse=True进行反向排序
>>>list=[3,4,2,6,1]
>>>sorted(list)
[1, 2, 3, 4, 6]
>>>sorted(list, reverse=True)
[6, 4, 3, 2, 1]

```



## `numpy.argsort()` 

`numpy.argsort()` 函数返回的是**数组值从小到大的索引值**。

```python
import numpy as np

x = np.array([3, 1, 2])
print('数组是：')
print(x)
# [3 1 2]
print('对 x 调用 argsort() 函数：')
y = np.argsort(x)
print(y)
#[1 2 0]
print('以排序后的顺序重构原数组：')
print(x[y])
# [1 2 3]
print('使用循环重构原数组：')
for i in y:
    print(x[i], end=" ")
    # 1 2 3

```

## `numpy.lexsort()`

`numpy.lexsort() ` 用于对多个序列进行排序。把它想象成对电子表格进行排序，每一列代表一个序列，排序时优先照顾靠后的列。

这里举一个应用场景：小升初考试，重点班录取学生按照总成绩录取。在总成绩相同时，数学成绩高的优先录取，在总成绩和数学成绩都相同时，按照英语成绩录取…… 这里，总成绩排在电子表格的最后一列，数学成绩在倒数第二列，英语成绩在倒数第三列。


```python
import numpy as np

nm = ('raju', 'anil', 'ravi', 'amar')
dv = ('f.y.', 's.y.', 's.y.', 'f.y.')
ind = np.lexsort((dv, nm))
print('调用 lexsort() 函数：')
print(ind)
print('\n')
print('使用这个索引来获取排序后的数据：')
print([nm[i] + ", " + dv[i] for i in ind])

调用 lexsort() 函数：
[3 1 0 2]


使用这个索引来获取排序后的数据：
['amar, f.y.', 'anil, s.y.', 'raju, f.y.', 'ravi, s.y.']

上面传入 np.lexsort 的是一个tuple，排序时首先排 nm，
顺序为：amar、anil、raju、ravi 。
综上排序结果为 [3 1 0 2]。

```

## `numpy.partition()`

```python
>>> a = np.array([3, 4, 2, 1])
>>> np.partition(a, 3)  
# 将数组 a 中所有元素（包括重复元素）从小到大排列，
# 3 表示的是排序数组索引为 3 的数字，比该数字小的排在该数字前面，
# 比该数字大的排在该数字的后面
array([2, 1, 3, 4])
>>>
>>> np.partition(a, (1, 3)) 
# 小于 1 的在前面，大于 3 的在后面，1和3之间的在中间
array([1, 2, 3, 4])

```



## `numpy.nonzero()`

`numpy.nonzero()` 函数返回输入数组中非零元素的索引。

```python
import numpy as np

a = np.array([[30, 40, 0], [0, 20, 10], [50, 0, 60]])
print(a)
# [[30 40  0]
#  [ 0 20 10]
#  [50  0 60]]
print('调用 nonzero() 函数：')
print(np.nonzero(a))
m=np.nonzero(a)
# (array([0, 0, 1, 1, 2, 2], dtype=int64), array([0, 1, 1, 2, 0, 2], dtype=int64))
#返回值的前后两部分数组，对应位置组合（0，0），（0，1）表示非0元素在原数组中的位置

#输出非0元素
print(a[m])
# [30 40 20 10 50 60]

```

## `numpy.where()`

```python
numpy.where(condition[, x, y])
```

该函数可以接受一个必选参数 condition，注意该参数必须是 array 型的，只不过元素是 true 或者是 false .

x,y是可选参数：如果条件为真，则返回x,如果条件为false，则返回y，注意condition、x、y三者必须要能够“广播”到相同的形状

返回结果：返回的是数组array或者是元素为array的tuple元组，如果只有一个condition，则返回包含array的tuple，如果是有三个参数，则返回一个array。

`numpy.where()` 函数**返回输入数组中满足给定条件的元素的索引**。

```python
import numpy as np 
 
x = np.arange(9.).reshape(3,  3)  
print ('我们的数组是：')
print (x)
print ( '大于 3 的元素的索引：')
y = np.where(x >  3)  
print (y)
print ('使用这些索引来获取满足条件的元素：')
print (x[y])

我们的数组是：
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]
大于 3 的元素的索引：
(array([1, 1, 2, 2, 2]), array([1, 2, 0, 1, 2]))
使用这些索引来获取满足条件的元素：
[4. 5. 6. 7. 8.]

```

## `np.piecewise()`

```python
numpy.piecewise(x, condlist, funclist, *args, **kw)
```

参数一 x:表示要进行操作的对象

参数二：condlist，表示要满足的条件列表，可以是多个条件构成的列表

参数三：funclist，执行的操作列表，参数二与参数三是对应的，当参数二为true的时候，则执行相对应的操作函数。

返回值：返回一个array对象，和原始操作对象x具有完全相同的维度和形状

```python
x = np.arange(0,10)
print(x)
xx=np.piecewise(x, [x < 4, x >= 6], [-1, 1])
print(xx)

[0 1 2 3 4 5 6 7 8 9]
[-1 -1 -1 -1  0  0  1  1  1  1]
```

即将元素中小于4的用-1替换掉，大于等于6的用1替换掉，其余的默认以0填充。其实这里的替换和填充就是function，这不过这里的function跟简单粗暴，都用同一个数替换了.

**使用lambda表达式**

```python
x = np.arange(0,10)
 
xxxx=np.piecewise(x, [x < 4, x >= 6], [lambda x:x**2, lambda x:x*100])
print(xxxx)

[  0   1   4   9   0   0 600 700 800 900]

```

## `numpy.extract()`

`numpy.extract()` 函数根据某个条件从数组中抽取 元素，返回满条件的元素。

`numpy.extract(条件，数组)：`如果满足某些指定条件，则返回input_array的元素。

```python
import numpy as np
# (1) 使用arange函数创建数组
a = np.arange(7)
# (2) 生成选择偶数元素的条件变量
condition = (a % 2) == 0
# (3) 使用extract函数基于生成的条件从数组中抽取元素
print "Even numbers", np.extract(condition, a)
# (4) 使用nonzero函数抽取数组中的非零元素
print "Non zero", np.nonzero(a)
```