# Pandas rename()和reindex()函数

## pandas.DataFrame.rename

更改行名列名**。传入的函数或字典值必须是1对1的**，没有包含在字典或者Series中的标签将保持原来的名称。字典中包含df中没有的标签，不会报错。

```python
DataFrame.rename(mapper=None, 
                 index=None, 
                 columns=None, 
                 axis=None, 
                 copy=True, 
                 inplace=False, 
                 level=None)
```

参数：

- `mapper`, `index`, `columns` : 映射的规则。

- `axis`：指定轴，可以是轴名称（'index'，'columns'）或数字（0,1），默认为index。

- `copy`：布尔值，默认为True，复制底层数据。

- `inplace`：布尔值，默认为False。指定是否返回新的DataFrame。如果为True，则在原df上修改，返回值为None。

- `level`：int或level name，默认为None。如果是MultiIndex，只重命名指定级别的标签。


**返回值：**

DataFrame



**两种修改的方法：**

- `(index=index_mapper, columns=columns_mapper, ...)`
- `(mapper, axis={'index', 'columns'}, ...)`

```python
In [1]: import numpy as np^M
   ...: import pandas as pd

In [2]: list_l = [[1, 3, 3, 5, 4], [11, 7, 15, 13, 9], [4, 2, 7, 9, 3], [15, 11, 12, 6, 11]]
   ...: index = ["2018-07-01", "2018-07-02", "2018-07-03", "2018-07-04"]
   ...: df = pd.DataFrame(list_l, index=index, columns=['a', 'b', 'c', 'd', 'e'])

In [3]: df
Out[3]:
             a   b   c   d   e
2018-07-01   1   3   3   5   4
2018-07-02  11   7  15  13   9
2018-07-03   4   2   7   9   3
2018-07-04  15  11  12   6  11

# 第一种修改方法
In [4]: df_rename = df.rename({'a': 'rename_a', 'b': 'rename_b', 'c': 'rename_c', 
                               'd': 'rename_d', 'e': 'rename_e'},
   ...:                       axis='columns')

In [5]: df_rename
Out[5]:
            rename_a  rename_b  rename_c  rename_d  rename_e
2018-07-01         1         3         3         5         4
2018-07-02        11         7        15        13         9
2018-07-03         4         2         7         9         3
2018-07-04        15        11        12         6        11





# 第二种修改方法
In [6]: df_rename = df.rename(index={"2018-07-01": 71, "2018-07-02": 72, 
                                     "2018-07-03": 73, "2018-07-04": 74},
                              
   ...:                       columns={'a': 'rename_a', 'b': 'rename_b', 
                                       'c': 'rename_c', 'd': 'rename_d', 
                                       'e': 'rename_e'})


                                       
In [7]: df_rename
Out[7]:
    rename_a  rename_b  rename_c  rename_d  rename_e
71         1         3         3         5         4
72        11         7        15        13         9
73         4         2         7         9         3
74        15        11        12         6        11
```

当` inplace=True` 时，返回值为 None，函数会在原df上进行修改。

```python
In [9]: df_rename = df.rename(index={"2018-07-01": 71, "2018-07-02": 72, "2018-07-03": 73, "2018-07-04": 74},^M
   ...:                       columns={'a': 'rename_a', 'b': 'rename_b', 'c': 'rename_c', 'd': 'rename_d', 'e': 'rename
   ...: _e'}, inplace=True)

In [10]: df
Out[10]:
    rename_a  rename_b  rename_c  rename_d  rename_e
71         1         3         3         5         4
72        11         7        15        13         9
73         4         2         7         9         3
74        15        11        12         6        11
```

## pandas.DataFrame.reindex

重建索引，对于索引没有对应值的，使用 NaN 或者指定的值填充。

```python
DataFrame.reindex(labels=None, index=None, columns=None, 
                  axis=None, method=None, 
                  copy=True, level=None, 
                  fill_value=nan, limit=None, tolerance=None)
```

参数：

- `method` : 用于填充重建索引的 DataFrame 中的缺失值的方法。（请注意：仅适用于具有单调递增/递减 index 的 DataFrames / Series。）

  默认：不填充

  - pad / ffill: 使用上一个有效观察填充
  - backfill / bfill: 使用下一个有效的观察值填充
  - nearest: 使用最靠近的有效值来填充空白

- `copy `: 布尔值，默认为 True，返回的是一个新的 df 对象（而不是在原对象上修改）。

- `fill_value` : 标量，默认为 np.NaN，可以是任意的值。用于填充缺失的值。

返回 :  


重建索引新 DataFrame 对象。

**DataFrame.reindex 支持两种方法：**

- `(index=index_labels, columns=column_labels, ...)`
- `(labels, axis={'index', 'columns'}, ...)`

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
 
list_l = [[1, 3, 3, 5, 4.], [11, 7, 15, 13, 9.1], [4, 2, 7, 9, 3.5], [15, 11, 12, 6, 11.1]]
index = ["2018-07-01", "2018-07-02", "2018-07-03", "2018-07-04"]
df = pd.DataFrame(list_l, index=index, columns=['a', 'b', 'c', 'd', 'e'])
print(df)
"""
             a   b   c   d     e
2018-07-01   1   3   3   5   4.0
2018-07-02  11   7  15  13   9.1
2018-07-03   4   2   7   9   3.5
2018-07-04  15  11  12   6  11.1
"""
 
# index
new_index = ["2018-07-04", "2018-07-05", "2018-07-06"]
df_reindex = df.reindex(index=new_index)
df_reindex2 = df.reindex(labels=new_index, axis="index")
print(df_reindex)
print(df_reindex2)
"""
               a     b     c    d     e
2018-07-04  15.0  11.0  12.0  6.0  11.1
2018-07-05   NaN   NaN   NaN  NaN   NaN
2018-07-06   NaN   NaN   NaN  NaN   NaN
"""
 
# columns
new_columns = ["c", "d", "e", "f"]
df_re = df.reindex(columns=new_columns)
df_re2 = df.reindex(labels=new_columns, axis="columns")
print(df_re)
print(df_re2)
"""
             c   d     e   f
2018-07-01   3   5   4.0 NaN
2018-07-02  15  13   9.1 NaN
2018-07-03   7   9   3.5 NaN
2018-07-04  12   6  11.1 NaN
"""
 
```

参考

<a href="https://blog.csdn.net/tz_zs/article/details/81355537" blank="">【pandas】 之 rename、reindex</a> 