# Pandas 缺失值处理

在实际应用中对于数据进行分析的时候，经常能看见缺失值，下如何利用pandas  来处理缺失值。常见的缺失值处理方式有，过滤、填充。

## 缺失值的判断 

pandas 使用浮点值 `NaN`(Not a Number)表示浮点数和非浮点数组中的缺失值，同时 python内置`None`值也会被当作是缺失值。

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200501111801.png"/>

## `DataFrame.dropna()`

```python
DataFrame.dropna(axis=0, 
                 how='any', 
                 thresh=None, 
                 subset=None, 
                 inplace=False
                )
```

- `axis `: 维度，axis=0 表示index行, axis=1表示columns列，默认为0

- `how`: "all"表示这一行或列中的元素全部缺失（为nan）才删除这一行或列，"any"表示这一行或列中只要有元素缺失，就删除这一行或列

- `thresh`:一行或一列中至少出现了thresh个才删除。

- `subset`：在某些列的子集中选择出现了缺失值的列删除，不在子集中的含有缺失值得列或行不会删除（有axis决定是行还是列）

- `inplace`：刷选过缺失值得新数据是存为副本还是直接在原数据上进行修改。

默认参数：删除行，只要有空值就会删除，不替换。

```python
df = pd.DataFrame({"name": ['Alfred', 'Batman', 'Catwoman'],
                   "toy": [np.nan, 'Batmobile', 'Bullwhip'],
                   "born": [pd.NaT, pd.Timestamp("1940-04-25"), pd.NaT]})

# print(df)
'''
       name        toy       born
0    Alfred        NaN        NaT
1    Batman  Batmobile 1940-04-25
2  Catwoman   Bullwhip        NaT
'''

print(df.dropna())
'''
     name        toy       born
1  Batman  Batmobile 1940-04-25
'''

print(df)
'''
       name        toy       born
0    Alfred        NaN        NaT
1    Batman  Batmobile 1940-04-25
2  Catwoman   Bullwhip        NaT
'''


#delete colums
print(df.dropna(axis=1) )#delete co
'''
       name
0    Alfred
1    Batman
2  Catwoman
'''

#"所有值全为缺失值才删除"
print(df.dropna(how='all'))
'''
       name        toy       born
0    Alfred        NaN        NaT
1    Batman  Batmobile 1940-04-25
2  Catwoman   Bullwhip        NaT
'''

#"至少出现过两个缺失值才删除"
print(df.dropna(thresh=2))
'''
       name        toy       born
1    Batman  Batmobile 1940-04-25
2  Catwoman   Bullwhip        NaT
'''

#"删除这个subset中的含有缺失值的行或列"
print (df.dropna(subset=['name', 'born']))
'''
     name        toy       born
1  Batman  Batmobile 1940-04-25
'''


```

## `DataFrame.fillna()`

```python
DataFrame.fillna(value=None, 
                 method=None, 
                 axis=None, 
                 inplace=False, 
                 limit=None, 
                 downcast=None, 
                 **kwargs
                )
```

函数作用：填充缺失值

- `value`:需要用什么值去填充缺失值

- `axis`:确定填充维度，从行开始或是从列开始

- `method`：ffill:用缺失值前面的一个值代替缺失值，如果axis =1，那么就是横向的前面的值替换后面的缺失值，如果axis=0，那么则是上面的值替换下面的缺失值。backfill/bfill，缺失值后面的一个值代替前面的缺失值。
  注意这个参数不能与value同时出现

- `limit`: 确定填充的个数，如果limit=2，则只填充两个缺失值。

```python

df = pd.DataFrame([[np.nan, 2, np.nan, 0],
                   [3, 4, np.nan, 1],
                   [np.nan, np.nan, np.nan, 5],
                   [np.nan, 3, np.nan, 4]],
                  columns=list('ABCD'))

print(df)
'''
     A    B   C  D
0  NaN  2.0 NaN  0
1  3.0  4.0 NaN  1
2  NaN  NaN NaN  5
3  NaN  3.0 NaN  4
'''

#"横向用缺失值前面的值替换缺失值"
print(df.fillna(axis=1, method='ffill'))
'''
     A    B    C    D
0  NaN  2.0  2.0  0.0
1  3.0  4.0  4.0  1.0
2  NaN  NaN  NaN  5.0
3  NaN  3.0  3.0  4.0
'''


#"纵向用缺失值上面的值替换缺失值"
print(df.fillna(axis=0,method='ffill'))
'''
     A    B   C  D
0  NaN  2.0 NaN  0
1  3.0  4.0 NaN  1
2  3.0  4.0 NaN  5
3  3.0  3.0 NaN  4
'''

print(df.fillna(0))
'''
     A    B    C  D
0  0.0  2.0  0.0  0
1  3.0  4.0  0.0  1
2  0.0  0.0  0.0  5
3  0.0  3.0  0.0  4
'''

```

不同的列用不同的值填充：,可以通过一个字典用`fillna`,实现对不同的列填充不同的值

```python
# 不同的列用不同的值填充：

values={'A':0,'B':1,'C':2,'D':3}
print(df.fillna(value=values))
'''
     A    B    C  D
0  0.0  2.0  2.0  0
1  3.0  4.0  2.0  1
2  0.0  1.0  2.0  5
3  0.0  3.0  2.0  4
'''

```

## DataFrame.isna()

判断是不是缺失值：

```python
df = pd.DataFrame({'age':[5, 6,np.NaN],
                   'born':[pd.NaT, pd.Timestamp('1939-05-27'),
                          pd.Timestamp('1929-05-27')],
                   'name':['alf', 'daes',''],
                   'toy':[None, 'asyeg','aued']    
})

df.isna()

	age		born	name	toy
0	False	True	False	True
1	False	False	False	False
2	True	False	False	False
```

`isnull` 同上。

```
df = pd.DataFrame([[np.nan, 2, np.nan, 0],
                   [3, 4, "", 1],
                   [np.nan, np.nan, np.nan, 5],
                   [np.nan, 3, "", 4]],
                  columns=list('ABCD'))

print(df)
'''
     A    B    C  D
0  NaN  2.0  NaN  0
1  3.0  4.0       1
2  NaN  NaN  NaN  5
3  NaN  3.0       4
'''

```

如上，缺失值是NAN，空值是没有显示。

替换空值代码：需要把含有空值的那一列提出来单独处理，然后在放进去就好。

```python
clean_z = df['C'].fillna(0)
clean_z[clean_z==''] = 'hello'
df['C'] = clean_z
print(df)
'''
     A    B      C  D
0  NaN  2.0      0  0
1  3.0  4.0  hello  1
2  NaN  NaN      0  5
3  NaN  3.0  hello  4
'''

```

