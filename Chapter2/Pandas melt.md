# Pandas.melt

数据分析的时候经常要把**宽数据**--->>**长数据**，有点像你们用excel 做透视跟逆透视的过程，直接看下面例子，希望有助于理解.

`pandas.melt` 使用参数：

```python
pandas.melt(frame, 
            id_vars=None, 
            value_vars=None, 
            var_name=None, 
            value_name='value', 
            col_level=None)
```

参数解释：

- frame:要处理的数据集。
- id_vars:不需要被转换的列名。
- value_vars:需要转换的列名，如果剩下的列全部都要转换，就不用写了。
- var_name和value_name是自定义设置对应的列名。
- col_level :如果列是MultiIndex，则使用此级别。

（问题来了：如果某些列没有包含在id_vars和value_vars中会怎么样呢？ 答:这些列的内容会被忽略）



Returns

- DataFrame



## Examples

```python
df = pd.DataFrame({'A': {0: 'a', 1: 'b', 2: 'c'},
                   'B': {0: 1, 1: 3, 2: 5},
                   'C': {0: 2, 1: 4, 2: 6}})
df
   A  B  C
0  a  1  2
1  b  3  4
2  c  5  6
```



转化 B 列

```python
pd.melt(df, id_vars=['A'], value_vars=['B'])
   A variable  value
0  a        B      1
1  b        B      3
2  c        B      5
```

转化 B，C 列

```python
pd.melt(df, id_vars=['A'], value_vars=['B', 'C'])
   A variable  value
0  a        B      1
1  b        B      3
2  c        B      5
3  a        C      2
4  b        C      4
5  c        C      6
```

The names of ‘variable’ and ‘value’ columns can be customized:

```python
pd.melt(df, id_vars=['A'], value_vars=['B'],
        var_name='myVarname', value_name='myValname')
   A myVarname  myValname
0  a         B          1
1  b         B          3
2  c         B          5
```



将数据转化，结合 seaborn 的 `FacetGrid()` 绘制组合图

```python
categorical_features = ["bodyType", "fuelType", "gearbox", "notRepairedDamage"]
data = Train_data[categorical_features]
f = pd.melt(data, value_vars=categorical_features)

f
```

<img src=".\img\image-20200907171043204.png" alt="image-20200907171043204" style="zoom:80%;" />



将其转化为两列，根据不同的标签绘制柱状图（分类，数量统计）

```python
def count_plot(x, **kwargs):
    sns.countplot(x=x)
    x = plt.xticks(rotation=90)

g = sns.FacetGrid(f, col="variable", col_wrap=2, size=6, sharex=False, sharey=False)
g = g.map(count_plot, "value")
```

<img src="F:\GithubWorkspace\GBooks\numpy-pandas-scipy\Chapter2\img\下载.png" alt="下载" style="zoom:80%;" />