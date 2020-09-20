# NumPy 降维和增维

## np.newaxis

`newaxis` 表示增加一个新的坐 标轴

```
import numpy as np
a = np.array([1,2,3])
print (a.shape,'\n',a)

结果为：
(3,)
[1 2 3]

a = np.array([1,2,3])[:,np.newaxis]
print (a.shape,'\n',a)

(3, 1)
[[1]
[2]
[3]]


```

和第一个程序相比，a的shape为（3，）现在为（3，1）变为二维数组了

```
a = np.array([1,2,3])[np.newaxis,:]
print (a.shape,'\n',a)

输出结果为：
(1, 3)
[[1 2 3]]

```

这个和第二个相比，好像和他是反的，相当于转置了，这是因为和`[np.newaxis,:]` 这个地方`np.newaxis` 放的位置有关，第二个程序放在[:,]的后面，相当于在原来的后面增加一个维度，所以变为(3,1)，而第三个则放在前面，则为(1,3)。放在前面是先逗号，再冒号，而放在后面是先冒号在逗号，不要弄错了，同时记得是中括号扩起来，不是小括号。

## ravel()、flatten()、squeeze()

numpy中的ravel()、flatten()、squeeze()都有将多维数组转换为一维数组的功能，区别：

- `ravel()`：如果没有必要，不会产生源数据的副本
- `flatten()`：返回源数据的副本
- `squeeze()`：只能对维数为1的维度降维

```python
numpy.ravel(a, order='C')
```

`numpy.ravel() ` vs `numpy.flatten()` 首先声明两者所要实现的功能是一致的（将多维数组降位一维），两者的区别在于返回拷贝（copy）还是返回视图（view）.

`numpy.flatten()` 返回一份拷贝，对拷贝所做的修改不会影响（reflects）原始矩阵，而`numpy.ravel()` 返回的是视图（view，也颇有几分C/C++引用reference的意味），会影响（reflects）原始矩阵。

