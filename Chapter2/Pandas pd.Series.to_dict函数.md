# Pandas pd.Series.to_dict()函数

```python
Series.to_dict(self, into=<class 'dict'>)
```

参数：

- **`orient`** : str {‘dict’, ‘list’, ‘series’, ‘split’, ‘records’, ‘index’}
  - `dict` (default) : {column -> {index -> value}}
  - `list`: {column -> [values]}
  - `series` : {column -> Series(values)}
  - `split` : {‘index’ -> [index], ‘columns’ -> [columns], ‘data’ -> [values]}
  - `records` : [{column -> value}, … , {column -> value}]
  - `index`: {index -> {column -> value}}

返回

**dict, list 或 collections.Mapping**

## 选择参数 `orient=dict`

dict也是默认的参数，下面的data数据类型为DataFrame结构, 会形成 {column -> {index -> value}}这样的结构的字典，可以看成是一种双重字典结构
- 单独提取每列的值及其索引，然后组合成一个字典
- 再将上述的列属性作为关键字（key），值（values）为上述的字典


查询方式为 ：`data_dict[key1][key2]`
-  data_dict 为参数选择orient=’dict’时的数据名
- key1 为列属性的键值（外层）
- key2 为内层字典对应的键值

```python
>>> df = pd.DataFrame({'col1': [1, 2],
...                    'col2': [0.5, 0.75]},
...                   index=['row1', 'row2'])
>>> df
      col1  col2
row1     1  0.50
row2     2  0.75
>>> df.to_dict()
{'col1': {'row1': 1, 'row2': 2}, 'col2': {'row1': 0.5, 'row2': 0.75}}
```

## 当关键字 `orient= list`

和1中比较相似，只不过内层变成了一个列表，结构为**{column -> [values]}**
查询方式为： `data_list[keys][index]`

- data_list 为关键字orient=’list’ 时对应的数据名
- keys 为列属性的键值，
- index 为整型索引，从0开始到最后

```python
>>> df.to_dict('list')
# {'col1': [1, 2], 'col2': [0.5, 0.75]}

df.to_dict('list')['col2'][1]
# 0.75
```

## 关键字参数`orient=series`

形成结构**{column -> Series(values)}**
调用格式为：`data_series[key1][key2]`或 `data_dict[key1]`

- data_series 为数据对应的名字
- key1 为列属性的键值
- key2 使用数据原始的索引（可选）

```python
>>> df.to_dict('series')
{'col1': row1    1
         row2    2
Name: col1, dtype: int64,
'col2': row1    0.50
        row2    0.75
Name: col2, dtype: float64}
```

## 关键字参数 `orient=split`

形成`{index -> [index], columns -> [columns], data -> [values]}`的结构，是将数据、索引、属性名单独脱离出来构成字典
调用方式有 `data_split[‘index’]`,`data_split[‘data’]`,`data_split[‘columns’]`

```python
df.to_dict('split')

{'index': ['row1', 'row2'],
 'columns': ['col1', 'col2'],
 'data': [[1, 0.5], [2, 0.75]]}

df.to_dict('split')['data']
# [[1, 0.5], [2, 0.75]]
```

## 当关键字`orient=records`

形成`[{column -> value}, … , {column -> value}]`的结构
整体构成一个列表，内层是将原始数据的每行提取出来形成字典
调用格式为`data_records[index][key1]`

```python
df.to_dict(orient='records')
# [{'col1': 1, 'col2': 0.5}, {'col1': 2, 'col2': 0.75}]
```

## 当关键字`orient=index`

形成`{index -> {column -> value}}`的结构，调用格式正好和’dict’ 对应的反过来

```python
df.to_dict(orient='index')

# {'row1': {'col1': 1, 'col2': 0.5}, 'row2': {'col1': 2, 'col2': 0.75}}
```

## 参考

<a href="https://blog.csdn.net/m0_37804518/article/details/78444110" blank="" >pandas to_dict 的用法</a> 