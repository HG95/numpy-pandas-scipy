# Numpy squeeze()函数

**语法**：`numpy.squeeze(a,axis = None)`

1）`a` 表示输入的数组； 

2）`axis` 用于指定需要删除的维度，但是指定的维度必须为单维度，否则将会报错； 

3）`axis `的取值可为None 或 int 或 tuple of ints, 可选。若axis为空，则删除所有单维度的条目； 

4）返回值： 数组 

5) 不会修改原数组；

**作用**：从数组的形状中删除单维度条目，即把shape中为1的维度去掉

场景：在机器学习和深度学习中，通常算法的结果是可以表示向量的数组（即包含两对或以上的方括号形式[[]]），如果直接利用这个数组进行画图可能显示界面为空（见后面的示例）。我们可以利用squeeze（）函数将表示向量的数组转换为秩为1的数组，这样利用matplotlib库函数画图时，就可以正常的显示结果了。



示例

```python
In [16]: import numpy as np

In [17]: a  = np.arange(10).reshape(1,10)

In [18]: a
Out[18]: array([[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]])

In [19]: a.shape
Out[19]: (1, 10)

In [20]: b = np.squeeze(a)^M
    ...: b
Out[20]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

In [21]: b.shape
Out[21]: (10,)
```



```python
In [22]: c  = np.arange(10).reshape(2,5)^M
    ...: c
Out[22]:
array([[0, 1, 2, 3, 4],
       [5, 6, 7, 8, 9]])

In [23]: np.squeeze(c)
Out[23]:
array([[0, 1, 2, 3, 4],
       [5, 6, 7, 8, 9]])
```

```python
In [24]: d  = np.arange(10).reshape(1,2,5)^M
    ...: d
Out[24]:
array([[[0, 1, 2, 3, 4],
        [5, 6, 7, 8, 9]]])

In [25]: d.shape
Out[25]: (1, 2, 5)

In [26]: np.squeeze(d)
Out[26]:
array([[0, 1, 2, 3, 4],
       [5, 6, 7, 8, 9]])

In [27]: np.squeeze(d).shape
Out[27]: (2, 5)
```

`np.squeeze()`函数可以删除数组形状中的单维度条目，即把shape中为1的维度去掉，但是对非单维的维度不起作用。



**matplotlib画图示例**

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200508103918.png"/>



参考

<a href="https://blog.csdn.net/zenghaitao0128/article/details/78512715" blank="">squeeze()函数</a> 