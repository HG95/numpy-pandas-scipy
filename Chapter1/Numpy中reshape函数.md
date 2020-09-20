# Numpy中reshape函数

**一般用法：`numpy.arange(n).reshape(a, b)`; 依次生成n个自然数，并且以a行b列的数组形式显示:**

```python
In [1]: 
np.arange(16).reshape(2,8) #生成16个自然数，以2行8列的形式显示
Out[1]: 
array([[ 0,  1,  2,  3,  4,  5,  6,  7],
       [ 8,  9, 10, 11, 12, 13, 14, 15]])

```

**特殊用法**:

`mat (or array).reshape(c, -1)`; 必须是矩阵格式或者数组格式，才能使用` .reshape(c, -1) `函数， 表示将此矩阵或者数组重组，以 c行d列的形式表示（-1的作用就在此，自动计算d：d=数组或者矩阵里面所有的元素个数/c, d必须是整数，不然报错）（reshape(-1, e) 即列数固定，行数需要计算）：

```python
In [2]: arr=np.arange(16).reshape(2,8)
out[2]:
 
In [3]: arr
out[3]:
array([[ 0,  1,  2,  3,  4,  5,  6,  7], 
       [ 8,  9, 10, 11, 12, 13, 14, 15]])
 
In [4]: arr.reshape(4,-1) #将arr变成4行的格式，列数自动计算的(c=4, d=16/4=4)
out[4]:
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15]])
 
In [5]: arr.reshape(8,-1) #将arr变成8行的格式，列数自动计算的(c=8, d=16/8=2)
out[5]:
array([[ 0,  1],
       [ 2,  3],
       [ 4,  5],
       [ 6,  7],
       [ 8,  9],
       [10, 11],
       [12, 13],
       [14, 15]])
 
In [6]: arr.reshape(10,-1) #将arr变成10行的格式，列数自动计算的(c=10, d=16/10=1.6 != Int)
out[6]:
ValueError: cannot reshape array of size 16 into shape (10,newaxis)

```

