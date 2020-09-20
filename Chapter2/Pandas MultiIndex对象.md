# Pandas MultiIndex对象 

分层/多级索引，因为它为一些非常复杂的数据分析和操作提供了可能性，特别是对于处理更高维度的数据。从本质上讲，它使你能在较低维度的数据结构(如Series（1d）和DataFrame（2d）)中存储和操作具有任意数量维度的数据。

## 创建MultiIndex

MultiIndex 对象是标准Index对象的扩展, 你可以将 MultiIndex 视为元组构成的列表，其中每个元组都是唯一的, 它与Index的区别是, Index 可以视为数字或者字符串构成的列表。可以从数组列表（使用`MultiIndex.from_arrays`），元组列表（使用`MultiIndex.from_tuples`）或交叉迭代集（使用`MultiIndex.from_product`）创建MultiIndex。当构造函数传递元组列表时，它将尝试返回 MultiIndex。以下示例演示了创建 MultiIndexes 的不同方法。

### `from_tuples`

创建一个元祖构成的列表

```python
arrays = [['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
            ['one', 'two', 'one', 'two', 'one', 'two', 'one', 'two']]

tuples = list(zip(*arrays))
print(tuples)
'''
[('bar', 'one'), ('bar', 'two'),
 ('baz', 'one'), ('baz', 'two'), 
 ('foo', 'one'), ('foo', 'two'), 
 ('qux', 'one'), ('qux', 'two')]

'''

```

使用 `from_tuples` 来创建 MultiIndex:

```python
arrays = [['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
            ['one', 'two', 'one', 'two', 'one', 'two', 'one', 'two']]

tuples = list(zip(*arrays))
print(tuples)
'''
[('bar', 'one'), ('bar', 'two'),
 ('baz', 'one'), ('baz', 'two'), 
 ('foo', 'one'), ('foo', 'two'), 
 ('qux', 'one'), ('qux', 'two')]

'''

```

### `from_arrays`

如果说 from_tuples 接受的参数是”`行`”的列表, 那么 `from_arrays` 接受的参数是就是”`列`”的列表:

```python
arrays = [['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
            ['one', 'two', 'one', 'two', 'one', 'two', 'one', 'two']]

index = pd.MultiIndex.from_arrays(arrays)
s = pd.Series(np.random.randn(8), index=index)

print(s)
'''
bar  one   -0.268434
     two   -0.026027
baz  one   -0.658945
     two    0.283218
foo  one    1.054412
     two    1.977076
qux  one   -0.563627
     two   -0.156421
dtype: float64
'''
```

不过为了简便, 我们通常可以直接在Series的构造函数中使用:

```python
arrays = [['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
            ['one', 'two', 'one', 'two', 'one', 'two', 'one', 'two']]

s = pd.Series(np.random.randn(8), index=arrays)
print(s)
'''
bar  one   -1.411561
     two    0.667025
baz  one   -0.079449
     two   -0.715518
foo  one   -1.844785
     two    0.257104
qux  one   -0.776653
     two   -1.159284
dtype: float64
'''

```



### `from_product`

假如我们有两个 list , 这两个 list 内的元素相互交叉, 两两搭配, 这就是两个 list 的product:

```python
lists = [['bar', 'baz', 'foo', 'qux'], ['one', 'two']]

index = pd.MultiIndex.from_product(lists, names=['first', 'second'])
s = pd.Series(np.random.randn(len(index)), index=index)
print(s)
'''
first  second
bar    one      -1.309958
       two       0.379085
baz    one       0.739266
       two      -0.165164
foo    one      -0.022698
       two      -0.006190
qux    one       0.299748
       two      -0.864639
dtype: float64
'''

```

### `MultiIndex.names`

你可以为 MultiIndex 的各个层起名字, 这就是 names 属性:

```python
print(s.index.names)
#['first', 'second']

s.index.names = ['FirstLevel', 'SecondLevel']
print(s.index.names)
#['FirstLevel', 'SecondLevel']

```

## MultiIndex可以作为`列名称`

Series 和 DataFrame 的列名称属性就是`columns`, 也可以是一个 MultiIndex 对象:

```python
df = pd.DataFrame(np.random.randn(3, 8), index=['A', 'B', 'C'], columns=index)
print(df)
'''
FirstLevel        bar                 baz  ...       foo       qux          
SecondLevel       one       two       one  ...       two       one       two
A            1.127256  1.453003  0.025833  ... -1.258916  0.711659 -1.460118
B            1.589573  2.057785  0.028412  ... -1.678021 -0.662083 -1.044907
C           -0.879705  0.730224 -0.003296  ... -0.446753 -1.694061  1.440663

[3 rows x 8 columns]
'''

```

### 获取各水平的值

方法`get_level_values`将返回特定级别的每个位置的`标签向量`：

```python
print(index.get_level_values(0))
'''
Index(['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
 dtype='object', name='FirstLevel')

'''

```

如果你给 index 设置了名称, 那么你可以直接使用名称来获取水平值:

```python
print(index.get_level_values('FirstLevel'))
'''
Index(['bar', 'bar', 'baz', 'baz', 'foo', 'foo', 'qux', 'qux'],
 dtype='object', name='FirstLevel')

'''

```

### 选择数据

这可能是MultiIndex最重要的功能之一。

```python
print(df)
'''
FirstLevel        bar                 baz  ...       foo       qux          
SecondLevel       one       two       one  ...       two       one       two
A            1.134195 -0.351198  0.218614  ... -0.755923  0.129988 -0.052183
B           -0.308971  1.399584 -0.894162  ... -1.022070  0.045872  1.539032
C           -0.399760  0.351285  1.069002  ... -0.771437  2.350300 -0.922563

[3 rows x 8 columns]
'''

```

获取 FirstLevel 是 bar 的所有数据

```python
print(df['bar'])
'''
SecondLevel       one       two
A            0.204079  0.635272
B            1.691298 -0.449358
C           -1.236855 -1.144767
'''

```

获取FirstLevel是bar, SecondLevel是one的所有数据:

```python
print(df['bar']['one'])
'''
A    0.121725
B    1.130435
C   -0.011153
Name: one, dtype: float64
'''

```

需要注意的是, 结果选择输出的结果的columns已经改变:

```python
print(df['bar'].columns)
#Index(['one', 'two'], dtype='object', name='SecondLevel')

```

如果你要选择第二层的列名为 one 的所有数据, 你需要借助 `xs` 方法:

```python
print(df.xs('bar', level=0, axis=1))
'''
SecondLevel       one       two
A           -1.493262 -0.704469
B            3.509268 -1.283146
C           -0.056974  0.710284
'''
print(df.xs('one', level=1, axis=1))
'''
FirstLevel       bar       baz       foo       qux
A           0.537299 -1.054771  0.144664 -0.940659
B          -0.560000 -0.952308 -1.667759 -1.480754
C           0.733805  0.930315 -0.144840 -1.261983
'''

```

或者使用名称代替数字:

```python
print(df.xs('one', level='SecondLevel', axis='columns'))
'''
FirstLevel       bar       baz       foo       qux
A           0.537299 -1.054771  0.144664 -0.940659
B          -0.560000 -0.952308 -1.667759 -1.480754
C           0.733805  0.930315 -0.144840 -1.261983
'''

```

`axis`, 它不仅可以用来选择列, 也可以用来选择行:

```python
print(s)
'''
FirstLevel  SecondLevel
bar         one            1.262375
            two            0.211678
baz         one           -0.207278
            two            0.386925
foo         one           -0.010342
            two           -1.775980
qux         one           -0.981227
            two           -2.159368
dtype: float64
'''

print(s.xs('one', level='SecondLevel', axis='index'))
'''
FirstLevel
bar    0.783906
baz    1.159497
foo   -1.361565
qux   -0.838874
dtype: float64
'''

```

### 选择行

把 df 进行转置, 然后看看一些选择行的操作:

```python
df = df.T
print(df)
'''
                               A         B         C
FirstLevel SecondLevel                              
bar        one          0.923159  3.412767 -2.821506
           two          2.641013  0.229025  1.251807
baz        one          0.900035  0.874848  0.246452
           two         -1.326872  0.647462 -0.088361
foo        one          1.730885 -0.732980 -0.373840
           two         -1.369826 -1.532940 -0.204242
qux        one          0.305318  0.929807 -0.331868
           two          1.110960 -0.869984  0.990428
'''

```

选择 FirstLevel 是 bar, SecondLevel 是 two 的数据:
```
print(df.loc[('bar', 'two')])
'''
A   -0.096414
B    0.796829
C   -0.571624
Name: (bar, two), dtype: float64
'''

```

**多重索引的标签要一元组的形式**`('bar', 'two')`，不能是列表的形式`['bar', 'two']`

下面的用法是等效的:

```python
print(df.loc['bar'].loc['two'])
'''
A   -0.755750
B    0.387714
C    1.164027
Name: two, dtype: float64
'''

```

选择行的同时也能选择列:

```python
print(df.loc[('bar', 'two'), 'A'])
#-0.5189738423458226

```

还能使用切片操作:

```python
print(df.loc['baz': 'foo'])
'''
                               A         B         C
FirstLevel SecondLevel                              
baz        one         -1.507232 -0.207591  1.242952
           two         -0.424180 -1.741234 -1.205756
foo        one          0.858520  1.594259 -1.314260
           two         -0.711255  0.356851 -0.276307
'''

```

或许, 使用更多的是这样:

```python
print(df.loc[('bar', 'two'): ('baz', 'two')])
'''
FirstLevel SecondLevel                              
bar        two         -1.293961 -0.931613  0.090003
baz        one         -0.509716 -0.802122  1.583681
           two         -0.613451  0.121745  0.895646
'''

```

推荐使用`xs`, 它可以使你的代码更容易被别人理解, 而且选择行和列都用统一的方式:

```python
print(df.xs('two', level='SecondLevel', axis='index'))
'''
                   A         B         C
FirstLevel                              
bar        -1.201396 -2.257291  0.831497
baz        -1.204905 -0.351232 -0.025386
foo         0.987691 -0.454322  0.679079
qux         0.813230  0.073436 -0.951928
'''

```

## MultiIndex对象属性

```python
m_index1=pd.Index([("A","x1"),("A","x2"),("B","y1"),("B","y2"),("B","y3")],name=["class1","class2"])
print(m_index1)
'''
MultiIndex([('A', 'x1'),
            ('A', 'x2'),
            ('B', 'y1'),
            ('B', 'y2'),
            ('B', 'y3')],
           names=['class1', 'class2'])
'''
df1=DataFrame(np.random.randint(1,10,(5,3)),index=m_index1)
print(df1)
'''
class1 class2         
A      x1      1  9  2
       x2      5  3  2
B      y1      8  8  6
       y2      9  2  2
       y3      5  6  8
'''
m_index=df1.index
print(m_index[0])
# ('A', 'x1')

print(m_index[1])
# ('A', 'x2')
```

调用`.get_loc()`和`.get_indexer()`获取标签的下标：

```python
print(m_index.get_loc(("A","x2")))  #1
print(m_index.get_indexer([("A","x2"),("B","y1"),"nothing"]))
#[ 1  2 -1]


```



## MultiIndex 对象使用多个 `Index` 对象保存索引中每一级的标签：

```python
print(m_index.levels[0])
print(m_index.levels[1])
'''
Index(['A', 'B'], dtype='object', name='class1')
Index(['x1', 'x2', 'y1', 'y2', 'y3'], dtype='object', name='class2')
'''

```

## MultiIndex 对象还有属性 `labels` 保存标签的下标：

```python
print(m_index.labels[0])
print(m_index.labels[1])
'''
[0 0 1 1 1]
[0 1 2 3 4]
'''

```

