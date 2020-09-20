# DataFrame.agg

```python
DataFrame.agg(func, axis=0, *args, **kwargs)
```

使用指定axis上的一个或多个操作Aggregate(聚合)。

参数

- **func** : `function, str, list `或 `dict`

  函数，用于聚合数据。如果是函数，

  则必须在传递`DataFrame`或传递到`DataFrame.apply`时工作。

  接受的组合是:

  ```python
  function
  string function name
  ```

  functions的list 和/或 function names, 例如， [np.sum, 'mean']

  axis labels的dict -> functions, function names 或 这样的list.

- **axis** : {0 or ‘index’, 1 或 ‘columns’}, 默认 0

  如果`0`或' `index` ':应用函数到每一列。

  如果`1`或‘`columns`’:应用函数到每一行。

- `*args`

    要传递给func的位置参数。

-  `**kwargs`

    要传递给func的关键字参数。

返回值：


DataFrame`, `Series` 或 `scalar


如果使用单个函数调用`DataFrame.agg`，则返回`Series`，

如果使用多个函数调用`DataFrame.agg`，

如果使用单个函数调用`Series.agg`则返回`DataFrame`，

如果使用多个函数调用`Series.agg`则返回标量， 

返回一个`Series`。

聚合操作总是在轴上执行，或者是`index`（默认）或列轴。 这种行为不同于

`numpy`聚合函数（`mean`，`median`，`prod`，`sum`，`std`，`var`），其中默认值是计算展平的聚合数组，例如`numpy.mean（arr_2d）` 而不是`numpy.mean（arr_2d，轴= 0）`。`agg`是`aggregate`的别名。 使用别名。



`agg`是聚合的别名。使用别名。

传递的用户定义函数将被传递一`Series`用于求值。

```python
df = pd.DataFrame([[1, 2, 3],
                   [4, 5, 6],
                   [7, 8, 9],
                   [np.nan, np.nan, np.nan]],
                  columns=['A', 'B', 'C'])
```

**在行上聚合这些函数**

```python
df.agg(['sum', 'min'])
        A     B     C
sum  12.0  15.0  18.0
min   1.0   2.0   3.0
```

**每个列有不同的聚合**

```python
df.agg({'A' : ['sum', 'min'], 'B' : ['min', 'max']})
        A    B
max   NaN  8.0
min   1.0  2.0
sum  12.0  NaN
```

**对列进行聚合**

```python
df.agg("mean", axis="columns")
0    2.0
1    5.0
2    8.0
3    NaN
dtype: float64
```



参考

- <a href="https://www.cjavapy.com/article/282/" target="_blank">Python pandas.DataFrame.agg函数方法的使用</a>

