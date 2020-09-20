# Pandas 数据去重 

数据去重可以使用 `duplicated()` 和 `drop_duplicates()` 两个方法。



## drop_duplicates()

`df.drop_duplicates(subset=None, keep='first', inplace=False)`

` drop_duplicate` 方法是对 DataFrame 格式的数据，去除特定列下面的重复行。返回DataFrame 格式的数据。

参数

- `subset`：可以指定传入**单个列标签或者一个列标签的列表**，默认是使用所有的列标签，即会删除一整行
- `keep`：有 {‘first’, ‘last’, False} 三个可供选择, 默认值 ‘first’，意味着除了第一个, 后面重复的全部删除，keep='first’表示保留第一次出现的重复行，是默认值。keep另外两个取值为"last"和False，分别表示保留最后一次出现的重复行和去除所有重复行。
- `inplace` : 返回是否替代过的值，默认False,即不改变原数据。

返回值

DataFrame

DataFrame with duplicates removed or None if `inplace=True`.


```python
data = pd.DataFrame({'A':[1,1,2,2],'B':['a','b','a','b']})

data.drop_duplicates('B','first',inplace=True)

data

	A	B
0	1	a
1	1	b

```

## duplicated()

DataFrame.duplicated（subset = None，keep =‘first’ ）返回boolean Series表示重复行

参数：

- subset：列标签或标签序列，可选
  仅考虑用于标识重复项的某些列，默认情况下使用所有列

- keep：{‘first’，‘last’，False}，默认’first’

  - first：标记重复，True除了第一次出现。

  - last：标记重复，True除了最后一次出现。

  - 错误：将所有重复项标记为True。 

返回值：Series   Boolean series for each duplicated rows.  重复值标记为 True, 不是重复值标记为Falese

​					

```python
data['B'].duplicated()

0    False
1    False
2     True
3     True
Name: B, dtype: bool



data[data['A'].duplicated()]


	A	B
2	2	a
3	2	b
```

