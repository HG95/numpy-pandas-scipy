# Pandas 数据排序 

有的时候我们可以要根据索引的大小或者值的大小对Series和DataFrame进行排名和排序。
根据条件对Series对象或DataFrame对象的值排序（`sorting`）和排名(`ranking`)是一种重要的内置运算。

使用 pandas 对象的：`sort_index()`/ `sort_values()`/ `rank()`方法。

## Series排序

`sort_index` 方法可以根据行或列的索引按照字典的顺序进行排序，返回一个已排 的新对象

### `sort_index` 按索引进行排序

```python
#定义一个Series
s = Series([1,2,3],index=["a","c","b"])
#对Series的索引进行排序，默认是升序
print(s.sort_index())
'''
a    1
b    3
c    2
'''
#对索引进行降序排序
print(s.sort_index(ascending=False))
'''
c    2
b    3
a    1
'''

```

### `sort_values`按值进行排序

```python
DataFrame.sort_values(by, 
                      axis=0, 
                      ascending=True, 
                      inplace=False, 
                      kind='quicksort', 
                      na_position='last'
                     )

```

- `axis`这个参数的默认值为`0`，匹配的是`index`，跨行进行排序，当`axis=1`时，匹配的是`columns`，跨列进行排序

- `by`这个参数要求传入一个字符或者是一个字符列表，用来指定按照`axis`的中的哪个元素来进行排序
- `ascending`这个参数的默认值是`True`，按照升序排序，当传入`False`时，按照降序进行排列
- `kind`这个参数表示按照什么样算法来进行排序，默认值是`quicksort`（快速排序），也可以传入`mergesort`（归并排序）或者是`heapsort`（堆排序），至于具体每种算法是如何实现的，我们这里按下不表，同样的，对于`inplace`这个参数我们也不做讨论对于涉及到的`In-place algorithm`（原地算法）感兴趣的可以看看[这里](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/In-place_algorithm)
  最后一个参数`na_position`是针对`DataFrame`中的空缺值的，默认值是`last`表示将空缺值放在排序的最后，也可以传入`first`放在最前：

```python
s = Series([np.nan,1,7,2,0],index=["a","c","e","b","d"])
#对Series的值进行排序，默认是按值的升序进行排序的
print(s.sort_values())
'''
d    0.0
c    1.0
b    2.0
e    7.0
a    NaN
'''
#对Seires的值进行降序排序
print(s.sort_values(ascending=False))
'''
e    7.0
b    2.0
c    1.0
d    0.0
a    NaN
'''
```
### NaN值会放在Series末尾

```python
se4=pd.Series([3,np.nan,-7,np.nan,5])
se4.sort_values()

2   -7.0
0    3.0
4    5.0
1    NaN
3    NaN
dtype: float64

```

## DataFrame排序

**通过**`axis`**参数可以对任意轴排序**

```python
df1=pd.DataFrame(np.arange(9).reshape(3,3),index=list("bac"),columns=list("yzx"))
print(df1)
'''
   y  z  x
b  0  1  2
a  3  4  5
c  6  7  8
'''

print(df1.sort_index())
'''
   y  z  x
a  3  4  5
b  0  1  2
c  6  7  8
'''

print(df1.sort_index(axis=1))
'''
   x  y  z
b  2  0  1
a  5  3  4
c  8  6  7
'''

```

**根据一个列的值来排序**

```python
df2=pd.DataFrame({'a':[20,3,3],'b':[1,-6,18]})
print(df2.sort_values(by='b'))
'''
    a   b
1   3  -6
0  20   1
2   3  18
'''

```

**对多个列来排序**

```python

df = DataFrame(np.arange(20).reshape(5,4),index=[3,1,2,4,6],columns=['d','c','a','b'])
print(df.sort_index(ascending=False)) # 降序排列
'''
    d   c   a   b
6  16  17  18  19
4  12  13  14  15
3   0   1   2   3
2   8   9  10  11
1   4   5   6   7
'''

```

## rank( )函数

`rank()`函数返回从小到大排序的下标

```python
DataFrame.rank(axis=0,
               method='average',
               numeric_only=None,
               na_option='keep',
               ascending=True,
               pct=False
              )
```

- **axis**：设置沿着哪个轴计算排名（0或者1)

- **numeric_only**：是否仅仅计算数字型的columns，布尔值

-  **na_option**：NaN值是否参与排序及如何排序（‘keep’，‘top'，’bottom'）

-  **ascending**：设定升序排还是降序排

-  **pct**：是否以排名的百分比显示排名（所有排名与最大排名的百分比）
- **method**：取值可以为'average'，'first'，'min'， 'max'，'dense'，
  - **"first":** 顾名思义，第一个，谁出现的位置靠前，谁的排名靠前。李四和王五的成绩都为30，但是李四出现在王五的前面，所以李四的排名靠前
  - **"min":** 当method=“min”时，成绩相同的同学，取在**顺序排名**中最小的那个排名作为该值的排名，李四和王五同学排名分别为2和3，那么当method为min时，取2和3的最小的那个作为第2名作为成绩30的排名。
  - "dense": 是密集的意思，即相同成绩的同学排名相同，其他依次加1即可。
  - average，成绩相同时，取顺序排名中所有名次之和除以该成绩的个数，即为该成绩的名次；比如上述排名中，30排名为2,3，那么 30的排名 = （2+3）/2=2.5，成绩为50的同学只有1个，且排名为1，那50的排名就位1/1=1。
  - max，和min一样也是跳跃排名的一种，成绩相同时取**顺序排名**中排名最大的作为该成绩的名次，在顺序排名中，30最大的排名为3，那么当参数为max时，30的排名=3，此时，李四和王五的排名都为第3名了。







- **默认情况下，rank是通过“为各组分配一个平均排名”的方式破坏平级关系的**

```python
In [120]:obj = pd.Series([7,-5,7,4,2,0,4])
In [121]:obj.rank()
Out [121]:
0    6.5
1    1.0
2    6.5
3    4.5
4    3.0
5    2.0
6    4.5
dtype: float64


```

在 obj 中，4和4的排名是第4名和第五名，取平均得4.5。7和7的排名分别是第六名和第七名，则其排名取平均得6.5

- 根据值在原数据中出现的顺序排名**

```python
In [122]:obj.rank(method='first')
Out [122]:
0    6.0
1    1.0
2    7.0
3    4.0
4    3.0
5    2.0
6    5.0
dtype: float64


```

- **按降序进行**

```python
In [123]:obj.rank(ascending=False, method='max')
Out [123]:
0    2.0
1    7.0
2    2.0
3    4.0
4    5.0
5    6.0
6    4.0
dtype: float64


```

- **若对DataFrame进行排序，则可根据axis指定要进行排序的轴**

```python
In [136]: frame=pd.DataFrame({'b':[5,7,-3,2],'a':[0,1,0,1],'c':[-2,5,8,-3]})

In [137]: frame
Out[137]:
   a  b  c
0  0  5 -2
1  1  7  5
2  0 -3  8
3  1  2 -3

In [138]: frame.rank(axis=0)
Out[138]:
     a    b    c
0  1.5  3.0  2.0
1  3.5  4.0  3.0
2  1.5  1.0  4.0
3  3.5  2.0  1.0

In [139]: frame.rank(axis=1)
Out[139]:
     a    b    c
0  2.0  3.0  1.0
1  1.0  3.0  2.0
2  2.0  1.0  3.0
3  2.0  3.0  1.0


```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200502102236.png"/>



参考：

<a href="https://zhuanlan.zhihu.com/p/35013079" blank="">pandas.sort_values方法</a> 

<a href="https://zhuanlan.zhihu.com/p/87593543" blank="">pandas的rank()函数</a> 