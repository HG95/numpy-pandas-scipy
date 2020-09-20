# Pandas Index对象 

Index 对象保存着索引标签数据，它可以快速找到标签对应的整数下标，其功能与Python的字典类似。

```python
dict1={"Province":["Guangdong","Beijing","Qinghai","Fujiang"],
      "year":[2018]*4,
      "pop":[1.3,2.5,1.1,0.7]}
df1=DataFrame(dict1)

print(df1)
'''
    Province  year  pop
0  Guangdong  2018  1.3
1    Beijing  2018  2.5
2    Qinghai  2018  1.1
3    Fujiang  2018  0.7
'''

```

调用`.columns`返回DataFrame对象的列索引（即所有列标签）：

```python
col_index=df1.columns
print(col_index)            
# Index(['Province', 'year', 'pop'], dtype='object')

print(col_index.values)     
# ['Province' 'year' 'pop']

```

调用`.index`

```python
ind_index=df1.index

print(ind_index.values) 
# RangeIndex(start=0, stop=4, step=1)

print(ind_index.values)     
#array([0, 1, 2, 3], dtype=int64)

```

Index 对象可当做一维数组，适合 Numpy 数组的下标运算，但 Index 对象只是可读，创建后不可修改。

```python
print(col_index[[1,2]])
print(ind_index[ind_index>1])

'''
Index(['year', 'pop'], dtype='object')
Int64Index([2, 3], dtype='int64')
'''
```

index 对象具有字典的映射功能，`.get_loc(value)`获得单值得下标，`.get_indexer(values)` 获得一组值得下标，当值不存在则返回-1：

```python
print(col_index.get_loc('pop'))
print(col_index.get_indexer(['pop','year']))
'''
2
[2 1]
'''

```

Index 对象调用 `Index()`来创建，可传递给 DataFrame 对象的参数 index 和columns。因为 Index 是不可变的，因此多个 DataFrame 对象的索引可以是同个Index对象。

```python
index=pd.Index(['a','b','c'])
df2=DataFrame(np.random.randint(1,10,(3,3)),index=index,columns=index)
print(df2)
'''
   a  b  c
a  3  5  3
b  9  2  3
c  6  3  3
'''

```

