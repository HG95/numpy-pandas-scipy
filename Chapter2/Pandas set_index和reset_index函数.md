# Pandas set_index()和reset_index()函数

## **set_index()**

作用：DataFrame可以通过set_index方法，将普通列设置为单索引/复合索引。

格式：`DataFrame.set_index(keys, drop=True, append=False, inplace=False, verify_integrity=False)`

参数含义：

- `keys`：列标签或列标签/数组列表，需要设置为索引的普通列
- `drop`：是否删除原普通列，默认为True，删除用作新索引的原普通列；
- `append`：是否变成复合索引，默认为False，即覆盖原索引，单索引；
- `inplace`：默认为False，适当修改DataFrame(不要创建新对象)；
- `verify_integrity`：默认为false，检查新索引的副本。否则，请将检查推迟到必要时进行。将其设置为false将提高该方法的性能。

### 参数`drop`

```python
# drop的使用：
import pandas as pd
df = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
print ('输出结果:\n',df)
print('------')
 
df_drop_t = df.set_index('A',drop=True) # drop默认True，普通列被用作索引后，原列删除
print (df_drop_t)
print('------')
 
df_drop_f = df.set_index('A',drop=False) # 普通列被用作索引后，原列保留
print (df_drop_f)
 
'''
输出结果:
     A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
------
     B   C   D
A
A0  B0  C0  D0
A1  B1  C1  D1
A2  B2  C2  D2
A3  B3  C3  D3
A4  B4  C4  D4
------
     A   B   C   D
A
A0  A0  B0  C0  D0
A1  A1  B1  C1  D1
A2  A2  B2  C2  D2
A3  A3  B3  C3  D3
A4  A4  B4  C4  D4
'''
```

### 参数 `append`

```python
# append的使用
 
import pandas as pd
df = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
 
print ('输出结果:\n',df)
print('------')
 
df_append_f = df.set_index('A', append=False) # append默认为False，普通列变为索引，并覆盖原索引，原索引被删除
print (df_append_f)
 
df_append_t = df.set_index('A', append=True) #  表示将普通列变为索引，原索引保留，变成了复合索引
print (df_append_t)
print('------')
 
'''
输出结果:
     A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
------
     B   C   D
A
A0  B0  C0  D0
A1  B1  C1  D1
A2  B2  C2  D2
A3  B3  C3  D3
A4  B4  C4  D4
------
       B   C   D
  A
0 A0  B0  C0  D0
1 A1  B1  C1  D1
2 A2  B2  C2  D2
3 A3  B3  C3  D3
4 A4  B4  C4  D4
 
'''
```

参数` inplace` 

```python
# inplace的使用，输出None
 
df = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
df_inplace_f = df.set_index('A', inplace=False) # inpla默认为False，表示适当修改DataFrame(不要创建新对象)
print ('输出结果：\n',df_inplace_f)
print('------')
 
df1 = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
 
df_inplace_t = df1.set_index('A',inplace=True) # 表示原地不动
print (df_inplace_t)
print (type(df_inplace_t))
 
'''
输出结果：
      B   C   D
A
A0  B0  C0  D0
A1  B1  C1  D1
A2  B2  C2  D2
A3  B3  C3  D3
A4  B4  C4  D4
------
None
<class 'NoneType'>
 
'''
```

## **reset_index()**

作用：reset_index可以还原索引为普通列，重新变为默认的整型索引

- （注：reset_index还原分为两种类型，第一种是对原DataFrame进行reset，第二种是对使用过set_index()函数的DataFrame进行reset）

格式：`DataFrame.reset_index(level=None, drop=False, inplace=False, col_level=0, col_fill=”)`

参数含义：

- `level`：int、str、tuple或list，默认无，仅从索引中删除给定级别。默认情况下移除所有级别。控制了具体要还原的那个等级的索引
- `drop`：索引被还原成普通列后，是否删掉列。默认为False，为False时则索引列会被还原为普通列，否则被还原后的的列又会被瞬间删掉；
- `inplace`：默认为false，适当修改DataFrame(不要创建新对象)；
- `col_level`：int或str，默认值为0，如果列有多个级别，则确定将标签插入到哪个级别。默认情况下，它将插入到第一级；
- `col_fill`：对象，默认‘’，如果列有多个级别，则确定其他级别的命名方式。如果没有，则重复索引名；



**对原DataFrame进行reset**

```python
# 一般情况下参数只使用到drop，这里只演示drop的使用
import pandas as pd
df = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
print ('输出结果\ndf:\n',df)
print('------')
 
df1 = df.reset_index(drop=False) # 默认为False，原有的索引不变,添加一列，列名index；
print (df1)
print('------')
 
df2 = df.reset_index(drop=True) # 索引被还原为普通列，瞬间又被删掉了，同时在原位置重置原始索引012...；
print (df2)
 
'''
输出结果
df:
     A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
------
   index   A   B   C   D
0      0  A0  B0  C0  D0
1      1  A1  B1  C1  D1
2      2  A2  B2  C2  D2
3      3  A3  B3  C3  D3
4      4  A4  B4  C4  D4
------
    A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
'''
```

**对使用过`set_index()`函数的DataFrame进行reset**

```python
# 一般情况下参数只使用到drop，这里只演示drop的使用
import pandas as pd
df = pd.DataFrame({ 'A': ['A0', 'A1', 'A2', 'A3','A4'],
                     'B': ['B0', 'B1', 'B2', 'B3','B4'],
                     'C': ['C0', 'C1', 'C2', 'C3','C4'],
                     'D': ['D0', 'D1', 'D2', 'D3','D4']})
print ('输出结果：\ndf:\n' ,df)
print('------')
newdf = df.set_index('A') # 这里的drop必需为True（默认为这里的drop必需为True），否则会报错ValueError: cannot insert A, already exists（意思是...只可意会不可言传哈哈）
print (newdf)
print('------')
 
newdf1 = newdf.reset_index(drop=False) #索引列会被还原为普通列
print (newdf1)
print('------')
 
newdf2 = newdf.reset_index(drop=True) #索引被还原为普通列，瞬间又被删掉了，同时在原位置重置原始索引；
print (newdf2)
 
'''
输出结果：
df:
     A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
------
     B   C   D
A
A0  B0  C0  D0
A1  B1  C1  D1
A2  B2  C2  D2
A3  B3  C3  D3
A4  B4  C4  D4
------
    A   B   C   D
0  A0  B0  C0  D0
1  A1  B1  C1  D1
2  A2  B2  C2  D2
3  A3  B3  C3  D3
4  A4  B4  C4  D4
------
    B   C   D
0  B0  C0  D0
1  B1  C1  D1
2  B2  C2  D2
3  B3  C3  D3
4  B4  C4  D4
'''
```

参考

<a href="https://www.shuzhiduo.com/A/mo5kPlpMdw/" blank=""> 区别 python-pandas库set_index、reset_index用法区别</a>

 