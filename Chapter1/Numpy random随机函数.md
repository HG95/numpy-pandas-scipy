# Numpy random函数

##  `numpy.random.RandomState()`

`numpy.random.RandomState()` 是一个伪随机数生成器。

伪随机数是用确定性的算法计算出来的似来自[0,1]均匀分布的随机数序列。并不真正的随机，但具有类似于随机数的统计特 征，如均匀性、独立性等。

```python
import numpy as np

rng = np.random.RandomState(0)
rng.rand(4)
# Out[377]: array([0.5488135 , 0.71518937, 0.60276338, 0.54488318])
rng = np.random.RandomState(0)
rng.rand(4)
# Out[379]: array([0.5488135 , 0.71518937, 0.60276338, 0.54488318])
```

0为随机种子，只要随机种子seed相同，产生的随机数序列就相同

因为是伪随机数，所以必须在 rng 这个变量下使用，如果不这样做，那么就得不到相同的随机数组了,即便你再次输入了`numpy.random.RandomState()`：

```python
prng = np.random.RandomState(123456789) # 定义局部种子
prng.rand(2, 4)

prng.chisquare(1, size=(2, 2)) # 卡方分布
prng.standard_t(1, size=(2, 3)) # t 分布
prng.poisson(5, size=10) # 泊松分布
```

## `numpy.random.seed()`

生成随机数的种子，使得每次生成随机数相同

`np.random.seed()` 的作用：使得随机数据可预测。 当我们设置相同的`seed`，每次生成的随机数相同。如果不设置seed，则每次会生成不同的

随机数` seed( )` 用于指定随机数生成时所用算法开始的整数值，如果使用相同的seed( )值， 则每次生成的随即数都相同，如果不设置这个值，则系统根据时间来自己选择这个值， 此时每次生成的随机数因时间差异而不同。

```python
In [26]: np.random.seed(0)
    ...: np.random.rand(5)
    ...:
Out[26]: array([ 0.5488135 ,  0.71518937,  0.60276338,  0.54488318,  0.4236548 ])
#不同的随机数种子下的rand生成的随机数组的值不等
In [27]: np.random.seed(1000)
    ...: np.random.rand(5)
    ...:
Out[27]: array([ 0.65358959,  0.11500694,  0.95028286,  0.4821914 ,  0.87247454])
#继续输入随机种子为1000下生成的随机数组
In [29]: np.random.seed(1000)
    ...: np.random.rand(5)
    ...:
Out[29]: array([ 0.65358959,  0.11500694,  0.95028286,  0.4821914 ,  0.87247454])

```

```python
from numpy import *
num=0
while(num<5):
    random.seed(15)
    print(random.random())
    num+=1

'''
0.8488176972685787
0.8488176972685787
0.8488176972685787
0.8488176972685787
0.8488176972685787
'''

num=0
random.seed(15)
while(num<5):
    print(random.random())
    num+=1
'''
0.8488176972685787
0.17889592492099848
0.05436321430643143
0.36153844608822294
0.27540092860641197
''' 

```

`random.seed(something)` 只能是一次有效。

## `numpy.random.rand()`

`numpy.random.rand(d0,d1...dn)`\

- `rand` 函数根据给定维度生成半开区间 [0,1)之间的数据，包含0，不包含1
- `dn` 表示每个维度
- 返回值为指定纬度的 `numpy.ndarray` 

```python
>>> np.random.rand(3, 3) # shape: 3*3

array([[0.94340617, 0.96183216, 0.88510322],
       [0.44543261, 0.74930098, 0.73372814],
       [0.29233667, 0.3940114 , 0.7167332 ]])

from numpy import random
x = random.rand(2, 3)
print(x)
[[ 0.1169922   0.08614147  0.17997144]
 [ 0.5694889   0.43067372  0.62135592]]
x, y = random.rand(2, 3)
print(x)
print(y)
[ 0.60527337  0.78765269  0.71884661]
[ 0.67420571  0.946359    0.7632273 ]

```

## `numpy.random.randint()`

`randint(low[, high, size, dtype])`

- 从区间[low,high）返回随机整形
- 参数：low为最小值，high为最大值，size为数组维度大小，dtype为数据类型，默认的- 数据类型是np.int
- high没有填写时，默认生成随机数的范围是[0，low)

```python
raw_user_item_mat = np.random.randint(0, 10, size=(3,4))     #指定生成随机数范围和生成的多维数组大小
print(raw_user_item_mat)
[[2 1 3 6]
 [8 9 1 6]
 [7 0 1 8]]


>>> np.random.randint(1, size = 10) # 返回[0, 1)之间的整数，所以只有0

array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0])

>>> np.random.randint(1, 5) # 返回[1, 5)之间随机的一个数字

2

```

## `np.random.randn()`

`numpy.random.randn(d0,d1,…,dn)`

- `randn` 函数返回一个或一组样本，具有标准正态分布。
- dn 表示每个维度
- 返回值为指定维度的 `numpy.ndarray` 数组元素来符合标准正态分布N(0,1)

```python
>>> np.random.randn() # 当没有输入参数时，仅返回一个值

-0.7377941002942127

>>> np.random.randn(3, 3)

array([[-0.20565666,  1.23580939, -0.27814622],
       [ 0.53923344, -2.7092927 ,  1.27514363],
       [ 0.38570597, -1.90564739, -0.10438987]])

>>> np.random.randn(3, 3, 3)

array([[[ 0.64235451, -1.64327647, -1.27366899],
        [ 0.69706885,  0.75246699,  2.16235763],
        [ 1.01141338, -0.19188666,  0.07684428]],

       [[ 1.34367043, -0.76837057,  0.27803575],
        [ 0.97007349,  0.41297538, -1.65008923],
        [-3.78282033,  0.67567421, -0.0753552 ]],

       [[-0.86540385,  0.14603592,  0.29318291],
        [-0.8167798 , -0.25492782, -0.58758   ],
        [ 0.02612474,  0.17882535, -0.95483945]]])


```

> 标准正态分布—-standard normal distribution；标准正态分布又称为u分布，是以0为均值、以1为标准差的正态分布，记为N（0，1）。

## `numpy.random.choice()`

`numpy.random.choice(a, size=None, replace=True, p=None)`

- 从给定的一位数组中生成一个随机样本
- a要求输入一维数组类似数据或者是一个int；size是生成的数组纬度，要求数字或元组；replace为布尔型，决定样本是否有替换；p为样本出现概率,p中概率和必须为1。

```python
#a为整数时，对应的一维数组是np.arange(a)
#第一个参数值5对应的a,即传入的数据组
#第二个参数3就是数组的size，传入单值时，数据维度是一维的
#此处将生成一个一维数据包含3个小于5的整数的数组
In [18]: np.random.choice(5,3)
Out[18]: array([2, 0, 3])
#给数组中每个数据出现的概率赋值
In [19]: np.random.choice(5, 3, p=[0.1, 0, 0.3, 0.6, 0])
Out[19]: array([3, 3, 0], dtype=int64)
#repalce参数为是否可以重复，当设置为FALSE时，不能出现重复的数据
In [21]: np.random.choice(5, 4, replace=False)
Out[21]: array([3, 2, 1, 4])
In [22]: np.random.choice(5, 5, replace=False)
Out[22]: array([4, 0, 3, 1, 2])
In [23]: np.random.choice(5, 3, replace=False, p=[0.1, 0, 0.3, 0.6, 0])
Out[23]: array([3, 0, 2])
#也可以传入非数字、字符串的数组
In [24]: demo_list = ['lenovo', 'sansumg','moto','xiaomi', 'iphone']

In [25]: np.random.choice(demo_list,size=(3,3))
Out[25]:
array([['lenovo', 'sansumg', 'sansumg'],
       ['sansumg', 'iphone', 'iphone'],
       ['lenovo', 'lenovo', 'xiaomi']],
      dtype='<U7')

```

## 打乱随机排列

### `np.random.shuffle(x)`

在原数组上进行，改变自身序列，无返回值。

```
import numpy as np

arr = np.arange(10)
print(arr)

np.random.shuffle(arr)
print(arr)

[0 1 2 3 4 5 6 7 8 9]
[5 6 9 7 3 2 8 4 1 0]

```

对多维数组进行打乱排列时，**默认是列维度**。

```python
arr=np.arange(12).reshape(3,4)
print(arr)
print('******')
np.random.shuffle(arr)
print(arr)

[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
******
[[ 8  9 10 11]
 [ 0  1  2  3]
 [ 4  5  6  7]]

```

### `np.random.permutation(x)`

- 可直接生成一个随机排列的数组

```python
ar=np.random.permutation(10)
print(ar)

#[9 6 5 8 4 1 7 2 3 0]

```

- 一维数组

```python
ar=np.random.permutation([1, 4, 9, 12, 15])
print(ar)
#[15  9 12  4  1]

```

- 多维数组

```python
arr=np.arange(9).reshape(3,3)
print(arr)
print('***********')
arr2=np.random.permutation(arr)
print(arr2)

[[0 1 2]
 [3 4 5]
 [6 7 8]]
***********
[[3 4 5]
 [6 7 8]
 [0 1 2]]



```

## 特定分布

`numpy.random` 能产生特定分布的随机数，如`normal`分布、`uniform`分布、`poisson`分布等
这些函数中前面几个参数是分布函数的参数，最后一个参数是`shape`
如正态分布`normal`就是均值和方差，`uniform` 就是上下界，泊松分布就是`λ`

### `np.random.uniform`

`np.random.uniform(low=0.0, high=1.0, size=None)`

作用：可以生成 [low,high) 中的随机数，可以是单个值，也可以是一维数组，也可以是多维数组
参数介绍：

- `low` : float 型，或者是数组类型的，默认为 0
- `high`: float 型，或者是数组类型的，默认为 1
- `size`: int 型，或元组，默认为空

```python
In[1]: import numpy as np

In[2]: np.random.uniform()  # 默认为0到1
Out[2]: 0.827455693512018

In[3]: np.random.uniform(1,5)
Out[3]: 2.93533586182789

In[4]: np.random.uniform(1,5,4)  #生成一维数组
Out[4]: array([ 3.18487512,  1.40233721,  3.17543152,  4.06933042])

In[5]: np.random.uniform(1,5,(4,3)) #生成4x3的数组
Out[5]: 
array([[ 2.33083328,  1.592934  ,  2.38072   ],
       [ 1.07485686,  4.93224857,  1.42584919],
       [ 3.2667912 ,  4.57868281,  1.53218578],
       [ 4.17965117,  3.63912616,  2.83516143]])

In[6]: np.random.uniform([1,5],[5,10])  
Out[6]: array([ 2.74315143,  9.4701426 ])
```

### `numpy.random.normal`

从正态（高斯）分布绘制随机样本。

`numpy.random.normal(loc=0.0, scale=1.0, size=None)`

- `loc`：float
      此概率分布的均值（对应着整个分布的中心centre）
- `scale`：float
      此概率分布的标准差（对应于分布的宽度，scale越大越矮胖，scale越小，越瘦高）
- `size`：int or tuple of ints
      输出的shape，默认为None，只输出一个值


## 参考

<a href="http://doc.codingdict.com/NumPy_v111/reference/routines.random.html" blank="">随机抽样</a> 

<a href="https://blog.csdn.net/lanchunhui/article/details/50163669" blank="">从np.random.normal()到正态分布的拟</a>  



