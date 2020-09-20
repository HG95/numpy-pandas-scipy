# DataFrame.nunique

```python
DataFrame.nunique(axis=0, dropna=True)
```

统计指定轴上不重复值得个数。

Return Series with number of distinct observations. Can ignore NaN values.

Parameters

- **axis** ：**{0 or ‘index’, 1 or ‘columns’}, default 0**

  The axis to use. 0 or ‘index’ for row-wise, 1 or ‘columns’ for column-wise.

- **dropna** ：bool, default True

  Don’t include NaN in the counts.

## Examples

```python
df = pd.DataFrame({'A': [1, 2, 3], 'B': [1, 1, 1]})
df.nunique()
A    3
B    1
dtype: int64
    
    
m = df.nunique(axis=0)
m.index
#Index(['A', 'B'], dtype='object')


m.values
#array([3, 1], dtype=int64)

df.nunique(axis=1)
0    1
1    2
2    2
dtype: int64
```