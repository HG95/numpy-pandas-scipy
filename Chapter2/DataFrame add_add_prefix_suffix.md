# DataFrame.add_add_prefix/suffix

```python
DataFrame.add_prefix(prefix)
```

为标签添加前缀

For Series, the row labels are prefixed. For DataFrame, the column labels are prefixed

参数：

- **prefix** ：str

  在每个标签前添加的字符串。

返回值：

- **Series or DataFrame**

  更新标签后的的新 Series 或 DataFrame。



**Examples**

```python
s = pd.Series([1, 2, 3, 4])
s
0    1
1    2
2    3
3    4
dtype: int64
```

```python
s.add_prefix('item_')
item_0    1
item_1    2
item_2    3
item_3    4
dtype: int64
```

```python
df = pd.DataFrame({'A': [1, 2, 3, 4], 'B': [3, 4, 5, 6]})
df
   A  B
0  1  3
1  2  4
2  3  5
3  4  6
```

```python
df.add_prefix('col_')
     col_A  col_B
0       1       3
1       2       4
2       3       5
3       4       6
```



添加后缀同样的用法。