# Pandas pd.get_dummies()函数

`get_dummies` 是利用 pandas 实现one hot encode的方式。详细参数请查看官方文档
[官方文档在这里](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.get_dummies.html)

```python
pandas.get_dummies(data,
                   prefix=None, 
                   prefix_sep='_', 
                   dummy_na=False, 
                   columns=None, 
                   sparse=False, 
                   drop_first=False
                  )
```

参数说明：

- `data` : array-like, Series, or DataFrame
  输入的数据
- `prefix` : string, list of strings, or dict of strings, default None
  get_dummies转换后，列名的前缀
- `columns `: list-like, default None
  指定需要实现类别转换的列名
- `dummy_na` : bool, default False
  增加一列表示空缺值，如果False就忽略空缺值
- `drop_first` : bool, default False
  获得k中的k-1个类别值，去除第一个



案例

```python
import pandas as pd
df = pd.DataFrame([  
            ['green' , 'A'],   
            ['red'   , 'B'],   
            ['blue'  , 'A']])  

df.columns = ['color',  'class'] 
pd.get_dummies(df) 
```

`get_dummies` 前：

```

	color	class
0	green	A
1	red		B
2	blue	A
```

`get_dummies` 后：

```
	color_blue	color_green	color_red	class_A		class_B
0	0			1			0			1			0
1	0			0			1			0			1
2	1			0			0			1			0
```

可以对指定列进行 `get_dummies`

```python
pd.get_dummies(df.color)
```

