# Series.cat

```python
Series.cat()
```

Series数据类型：Category

**Examples**

转化为 Category 类型

```python
s = pd.Series(list("abbccc")).astype("category")
s
0    a
1    b
2    b
3    c
4    c
5    c
dtype: category
Categories (3, object): ['a', 'b', 'c']
```

查看类别

```
s.cat.categories
Index(['a', 'b', 'c'], dtype='object')
```



按照先后顺序，重新命名

```python
s.cat.rename_categories(list("cba"))
0    c
1    b
2    b
3    a
4    a
5    a
dtype: category
Categories (3, object): ['c', 'b', 'a']
```

增加类别：

```python
s.cat.add_categories(["d", "e"])
0    a
1    b
2    b
3    c
4    c
5    c
dtype: category
Categories (5, object): ['a', 'b', 'c', 'd', 'e']
```

删除列别

```python
s.cat.remove_categories(["a", "c"])
0    NaN
1      b
2      b
3    NaN
4    NaN
5    NaN
dtype: category
Categories (1, object): ['b']
```



删除无用得类别：

```python
s1 = s.cat.add_categories(["d", "e"])
s1.cat.remove_unused_categories()
0    a
1    b
2    b
3    c
4    c
5    c
dtype: category
Categories (3, object): ['a', 'b', 'c']
```

## 案例

增加类别，并将缺失值填充为新得类别

```python
if Train_data[c].isnull().any():
    Train_data[c] = Train_data[c].cat.add_categories(["MISSING"])
    Train_data[c] = Train_data[c].fillna("MISSING")
```



