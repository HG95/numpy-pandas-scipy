# Pandas 众数mode

```python
DataFrame.mode(axis=0, numeric_only=False, dropna=True)
```

返回指定行/列的众数，可能是多个值。

参数：

- **axis** ：**{0 or ‘index’, 1 or ‘columns’}, default 0**

  The axis to iterate over while searching for the mode:

  - 0 or ‘index’ : get mode of each column
  - 1 or ‘columns’ : get mode of each row.

- **numeric_only** ：**bool** **default False**

  若 为 True 则只对数字进行众数计算。

  

- **dropna** ：bool, default True

  不考虑NaN/NaT的计数。

返回值： **DataFrame** 每列或每行的众数。



```python
>>> df = pd.DataFrame({'A': [1, 2, 1, 2, 1, 2, 3]})
>>> df.mode()
   A
0  1
1  2
# 1和2 都出现了三次，所以返回的是这两个数
```

**Examples**

```python
df = pd.DataFrame([('bird', 2, 2),
                   ('mammal', 4, np.nan),
                   ('arthropod', 8, 0),
                   ('bird', 2, np.nan)],
                  index=('falcon', 'horse', 'spider', 'ostrich'),
                  columns=('species', 'legs', 'wings'))
df
           species  legs  wings
falcon        bird     2    2.0
horse       mammal     4    NaN
spider   arthropod     8    0.0
ostrich       bird     2    NaN
```

```python
df.mode()
  species  legs  wings
0    bird   2.0    0.0
1     NaN   NaN    2.0

# wings 有两个众数，其它的只有一个，空缺的位置用NaN 填充
```

```python
df.mode(dropna=False)
  species  legs  wings
0    bird     2    NaN
```

只对数字进行计算

```python
df.mode(numeric_only=True)
   legs  wings
0   2.0    0.0
1   NaN    2.0
```

对行/列计算

```python
df.mode(axis='columns', numeric_only=True)
           0    1
falcon   2.0  NaN
horse    4.0  NaN
spider   0.0  8.0
ostrich  2.0  NaN
```



