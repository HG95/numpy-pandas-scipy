# DataFrame.select_dtypes

根据列的 `dtypes`返回DataFrame的列的子集。

```python
DataFrame.select_dtypes(include=None, exclude=None)
```

参数：

- **include, exclude** ：标量或数据类型构成的数组

  `include` 要选取的，`exclude` 要排除的

返回值：

- **DataFrame** 

  包括include中的dtypes和exclude中的dtypes的DataFrame子集。



**Notes** 

- To select all *numeric* types, use `np.number` or `'number'` 
- To select strings you must use the `object` dtype, but note that this will return *all* object dtype columns
- To select datetimes, use `np.datetime64`, `'datetime'` or `'datetime64'`
- To select Pandas categorical dtypes, use `'category'`
- To select timedeltas, use `np.timedelta64`, `'timedelta'` or `'timedelta64'`
- See the [numpy dtype hierarchy](https://numpy.org/doc/stable/reference/arrays.scalars.html)



**Examples**

```python
df = pd.DataFrame({'a': [1, 2] * 3,
                   'b': [True, False] * 3,
                   'c': [1.0, 2.0] * 3})
df
        a      b  c
0       1   True  1.0
1       2  False  2.0
2       1   True  1.0
3       2  False  2.0
4       1   True  1.0
5       2  False  2.0
```

```python
df.select_dtypes(include='bool')
   b
0  True
1  False
2  True
3  False
4  True
5  False
```

```python
df.select_dtypes(include=['float64'])
   c
0  1.0
1  2.0
2  1.0
3  2.0
4  1.0
5  2.0
```

```python
df.select_dtypes(exclude=['int64'])
       b    c
0   True  1.0
1  False  2.0
2   True  1.0
3  False  2.0
4   True  1.0
5  False  2.0
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818151735.png" alt="image-20200818151423199" style="zoom:80%;" />

假设你仅仅需要选取数值型的列，那么你可以使用 `select_dtypes()`函数：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818151748.png" alt="image-20200818151500702" style="zoom:80%;" />

这包含了int和float型的列。

你还可以选取多种数据类型，只需要传递一个列表即可：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818151742.png" alt="image-20200818151538212" style="zoom:80%;" />

你还可以用来排除特定的数据类型：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818151754.png" alt="image-20200818151607499" style="zoom:80%;" />