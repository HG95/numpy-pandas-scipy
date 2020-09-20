# Pandas pivot函数 

```python
DataFrame.pivot(index=None, 
                columns=None, 
                values=None
               )
```

返回按给定索引/列值组织的重新构造的`DataFrame`。

根据列值重塑数据(生成一个 `"pivot"` 表)。使用来自指定索引/列的惟一值来形成结果`DataFrame`的轴。此函数不支持数据聚合，多个值将导致列中的多索引。

-  `index` ：`str`或 `object`, 可选用于制作新`frame`索引的列。如果为`None`，则使用现有索引。
- `columns` ：`str`或`object`位置参数传递给`func`。
- `values` ：`str`, `object` 或 之前的列表, 可选于填充新frame值的列。如果未指定，将使用所有剩余的列，并且结果将具有按层次结构索引的列。

返回


DataFrame   返回调整后的`DataFrame`。

**例子**

```python
import pandas as pd
df = pd.DataFrame({'foo': ['one', 'one', 'one', 'two', 'two',
                            'two'],
                    'bar': ['A', 'B', 'C', 'A', 'B', 'C'],
                    'baz': [1, 2, 3, 4, 5, 6],
                    'zoo': ['x', 'y', 'z', 'q', 'w', 't']})
```

df 

```
	foo	bar	baz	zoo
0	one	A	1	x
1	one	B	2	y
2	one	C	3	z
3	two	A	4	q
4	two	B	5	w
5	two	C	6	t
```

```python
df.pivot(index='foo', columns='bar', values='baz')
# 或  df.pivot(index='foo', columns='bar')['baz']
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200502111404.png"/>

查看多列数据

```python
df.pivot(index='foo', columns='bar', values=['baz', 'zoo'])
```



<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200502111538.png"/>


如果存在重复项，则会引发ValueError



参考

<a href="https://www.cjavapy.com/article/644/" blank="">pandas.DataFrame.pivot函数</a> 