# Pandas isin索引和~反向索引

## `isin`

###### 1、直接根据条件进行索引，isin()接受一个列表，判断该列中元素是否在列表中

```python
DataFrame.isin(values)
```

```python
df = pd.DataFrame({'num_legs': [2, 4], 'num_wings': [2, 0]},
                  index=['falcon', 'dog'])
df
        num_legs  num_wings
falcon         2          2
dog            4          0


# 当values是一个列表时，检查DataFrame中的每个值是否都存在于列表中
df.isin([0, 2])
        num_legs  num_wings
falcon      True       True
dog        False       True
```

###### 2、通过字典的形式传递多个条件{‘某列’:[条件],‘某列’:[条件],}

当values是dict时，我们可以传递值来分别检查每个列：

```python
df.isin({'num_wings': [0, 3]})
        num_legs  num_wings
falcon     False      False
dog        False       True
```

###### 3、When `values` is a Series or DataFrame the index and column must match

索引行和列必须同时匹配

```python
other = pd.DataFrame({'num_legs': [8, 2], 'num_wings': [0, 2]},
                     index=['spider', 'falcon'])
df.isin(other)
        num_legs  num_wings
falcon      True       True
dog        False      False
```



###### 4、根据多条件进行索引，此时用&（交集）或者|（并集）进行连接

```
import numpy as np
import pandas as pd
df=pd.DataFrame(np.random.randn(4,4),columns=['A','B','C','D'])
df
Out[189]: 
          A         B         C         D
0  0.289595  0.202207 -0.850390  0.197016
1  0.403254 -1.287074  0.916361  0.055136
2 -0.359261 -1.266615 -0.733625 -0.790208
3  0.164862 -0.649637  0.716620  1.447703
df['E'] = ['aa', 'bb', 'cc', 'cc']
df
Out[191]: 
          A         B         C         D   E
0  0.289595  0.202207 -0.850390  0.197016  aa
1  0.403254 -1.287074  0.916361  0.055136  bb
2 -0.359261 -1.266615 -0.733625 -0.790208  cc
3  0.164862 -0.649637  0.716620  1.447703  cc
```

```python
df[df.E.isin(['aa'])|df.E.isin(['cc'])]
Out[194]: 
          A         B         C         D   E
0  0.289595  0.202207 -0.850390  0.197016  aa
2 -0.359261 -1.266615 -0.733625 -0.790208  cc
3  0.164862 -0.649637  0.716620  1.447703  cc
df[df.E.isin(['aa'])]
Out[195]: 
          A         B        C         D   E
0  0.289595  0.202207 -0.85039  0.197016  aa

```

### `~`相当于 `isnotin`

```python
df[~(df.E=='cc')]
Out[202]: 
          A         B         C  D   E
0  0.289595  0.202207 -0.850390  1  aa
1  0.403254 -1.287074  0.916361  2  bb

```

