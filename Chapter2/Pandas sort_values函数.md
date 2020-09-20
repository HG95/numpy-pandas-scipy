# Pandas sort_values()函数

pandas中的`sort_values()`函数原理类似于SQL中的`order by`，可以将数据集依照某个字段中的数据进行排序，该函数即可根据指定列数据也可根据指定行的数据排序。

## **`sort_values()`函数的具体参数**

```python
DataFrame.sort_values(by=‘##’,
                      axis=0,
                      ascending=True, 
                      inplace=False, 
                      na_position=‘last’)
```

参数	

- `by`	指定列名(axis=0或’index’)或索引值(axis=1或’columns’)
- `axis`	若axis=0或’index’，则按照指定列中数据大小排序；若axis=1或’columns’，则按照指定索引中数据大小排序，**默认axis=0**
- `ascending`	是否按指定列的数组升序排列，默认为True，即升序排列
- `inplace`	是否用排序后的数据集替换原来的数据，默认为False，即不替换
- `na_position`	{‘first’,‘last’}，设定缺失值的显示位置


## **sort_values用法举例**

- 创建数据框

```python
#利用字典dict创建数据框
import numpy as np
import pandas as pd
df=pd.DataFrame({'col1':['A','A','B',np.nan,'D','C'],
                 'col2':[2,1,9,8,7,7],
                 'col3':[0,1,9,4,2,8]
})
print(df)

>>>
  col1  col2  col3
0    A     2     0
1    A     1     1
2    B     9     9
3  NaN     8     4
4    D     7     2
5    C     7     8

```

- 依据第一列排序，并将该列空值放在首位

```python
#依据第一列排序，并将该列空值放在首位
print(df.sort_values(by=['col1'],na_position='first'))
>>>
  col1  col2  col3
3  NaN     8     4
0    A     2     0
1    A     1     1
2    B     9     9
5    C     7     8
4    D     7     2

```

- 依据第二、三列，数值降序排序

```python
#依据第二、三列，数值降序排序
print(df.sort_values(by=['col2','col3'],ascending=False))
>>>
  col1  col2  col3
2    B     9     9
3  NaN     8     4
5    C     7     8
4    D     7     2
0    A     2     0
1    A     1     1

```

- 根据第一列中数值排序，按降序排列，并替换原数据

```python
#根据第一列中数值排序，按降序排列，并替换原数据
df.sort_values(by=['col1'],ascending=False,inplace=True,
                     na_position='first')
print(df)
>>>
  col1  col2  col3
3  NaN     8     4
4    D     7     2
5    C     7     8
2    B     9     9
1    A     1     1
0    A     2     0

```

- 按照索引值为0的行，即第一行的值来降序排序

```python
x = pd.DataFrame({'x1':[1,2,2,3],'x2':[4,3,2,1],'x3':[3,2,4,1]}) 
print(x)
#按照索引值为0的行，即第一行的值来降序排序
print(x.sort_values(by =0,ascending=False,axis=1))
>>>
   x1  x2  x3
0   1   4   3
1   2   3   2
2   2   2   4
3   3   1   1
   x2  x3  x1
0   4   3   1
1   3   2   2
2   2   4   2
3   1   1   3

```

# sort_index（）

Series 的 `sort_index(ascending=True) `方法可以对 index 进行排序操作，ascending 参数用于控制升序或降序，默认为升序。

和 `sort_values()` 的用法相同。