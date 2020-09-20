# Pandas 轴旋转stack和unstack

pandas 的 DataFrame 的轴旋转操作，`stack` 和 `unstack`

首先，要知道以下五点：

1. `stack`：将数据的列“旋转”为行
2. `unstack`：将数据的行“旋转”为列
3. `stack和unstack`默认操作为最内层
4. `stack`和`unstack`默认旋转轴的级别将会成果结果中的最低级别（最内层）
5. `stack`和`unstack`为一组逆运算操作


- 创建DataFrame,行索引名为state，列索引名为number

```python
import pandas as pd
import numpy as np
data = pd.DataFrame(np.arange(6).reshape((2, 3)),
                    index=pd.Index(['Ohio', 'Colorado'], name='state'),
                    columns=pd.Index(['one', 'two', 'three'], name='number'))
data
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514213506.png"/>

- 将DataFrame的列旋转为行，即`stack`操作。

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514213632.png"/>

从结果来理解上述点4**`stack` 操作后将列索引number旋转为行索引，并且置于行索引的最内层（外层为索引state），也就是将旋转轴（number）的结果置于 最低级别。** 

- 将DataFrame的行旋转为列，即`unstack`操作。

```python
result.unstack()
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514213856.png"/>

`unstack`操作默认将内层索引number旋转为列索引。
同时，也可以指定分层级别或者索引名称来指定操作级别，下面做法同样会得到上面的结果。

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514214141.png"/>

- `stack` 和 `unstack` 逆运算

```python
s1 = pd.Series([0,1,2,3],index=list('abcd'))
s2 = pd.Series([4,5,6],index=list('cde'))
data2 = pd.concat([s1,s2],keys=['one','two'])
data2
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514214341.png"/>

```python
data2.unstack()
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514214417.png"/>

```python
data2.unstack().stack()
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514214512.png"/>

参考

<a href="https://blog.csdn.net/Asher117/article/details/85047899" blank="">【Python】pandas轴旋转stack和unstack用法详解</a> 