# Pandas Apply函数 

pandas 的 `apply()` 函数可以作用于 `Series` 或者整个 `DataFrame`，功能也是自动遍历整个 `Series` 或者 `DataFrame`, 对每一个元素运行指定的函数。

```python
DataFrame.apply(func, 
                axis=0, 
                broadcast=False, 
                raw=False, 
                reduce=None, 
                args=(), 
                **kwds
               )
```

该函数最有用的是第一个参数，这个参数是函数，相当于`C/C++`的函数指针。

- **func** : function作用于每一列或行。

- **axis** : {0 或 ‘index’, 1 或 ‘columns’}, 默认 0

  函数所应用的轴:

  0 或 ‘index’: 对每一列应用函数。

  1 或 ‘columns’: 对每一行应用函数。

- **broadcast** : `bool`, 可选  仅与聚合函数相关:

  `False` 或 `None` : 返回一个Series，该Series的长度是索引的长度或列的数量(基于axis参数)

  **True** : 结果将广播到框架的原始形状，原始索引和列将保留。

  从0.23.0版本开始就不推荐使用:这个参数将在将来的版本中被删除，取而代之的是`result_type= ' broadcast '`。

- **raw** : bool, 默认 False

  False : 将每一行或每一列作为一个Series传递给函数。

  True : t传递的函数将接收ndarray对象。如果您只是应用一个NumPy约简函数，这将获得更好的性能。

- **reduce** : `bool `或 `None`, 默认 `None`

  试着使用减量程序。如果`DataFrame`为空，`apply`将使用`reducto`确定结果应该是一个Series还是一个`DataFrame`。如果`reduce=None`(缺省值)，`apply`的返回值将通过在空序列上调用`func`来猜测(注意:在猜测时，`func`引发的异常将被忽略)。如果`reduce=True`，则始终返回一个Series，如果`reduce=False`，则始终返回一个`DataFrame`。

  从0.23.0版本开始就不推荐使用:这个参数将在将来的版本中被删除，取而代之的是`result_type='reduce'`。

- **result_type** : {‘expand’, ‘reduce’, ‘broadcast’, None}, 默认 `None`

  这些只在`axis=1`(列)时起作用:

  ‘expand’ : 类似列表的结果将转换为列。

  ‘reduce’ : 如果可能，返回一个Series，而不是展开类似列表的结果。这是‘expand’的反义词。

  ‘broadcast’ : 结果将广播到`DataFrame`的原始形状，保留原始索引和列。

  默认行为(None)取决于应用函数的返回值:类似列表的结果将作为这些结果的Series返回。但是，如果`apply`函数返回一个Series，这些列就会展开为列。



- **args** : `tuple`

  除了`array`/`series`外，还要传递给func的位置参数。

- ***\*kwds**

  要作为关键字参数传递给func的其他关键字参数。

这个函数需要自己实现，函数的传入参数根据axis来定，比如 axis = 1，就会把一行数据作为Series的数据结构传入给自己实现的函数中，我们在函数中实现对Series不同属性之间的计算，返回一个结果，则`apply` 函数会自动遍历每一行 DataFrame 的数据，最后将所有结果组合成一个Series数据结构并返回。

## Series.apply()

举一个例子，现在有这样一组数据，学生的考试成绩：

```
  Name Nationality  Score
   张           汉    400
   李           回    450
   王           汉    460

```

如果民族不是汉族，则总分在考试分数上再加 5 分，现在需要用 pandas 来做这种计算，我们在 Dataframe 中增加一列。当然如果只是为了得到结果， `numpy.where()` 函数更简单，这里主要为了演示 `Series.apply()` 函数的用法。

```python
import pandas as pd

df = pd.read_csv("studuent-score.csv")
df['ExtraScore'] = df['Nationality'].apply(lambda x : 5 if x != '汉' else 0)
df['TotalScore'] = df['Score'] + df['ExtraScore']

```

`apply()` 函数当然也可执行 python 内置的函数，比如我们想得到 Name 这一列字符的个数，如果用 `apply()` 的话：

```python
df['NameLength'] = df['Name'].apply(len)

```

## DataFrame.apply()

`DataFrame.apply()` 函数则会遍历每一个元素，对元素运行指定的 function。比如下面的示例：

```python
import pandas as pd
import numpy as np

matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

df = pd.DataFrame(matrix, columns=list('xyz'), index=list('abc'))
df.apply(np.square)

```

对 df 执行 `square()` 函数后，所有的元素都执行平方运算：

```
    x   y   z
a   1   4   9
b  16  25  36
c  49  64  81

```

如果只想 `apply()` 作用于指定的行和列，可以用行或者列的 `name` 属性进行限定。比如下面的示例将 x 列进行平方运算：

```python
df.apply(lambda x : np.square(x) if x.name=='x' else x)


	x  y  z
a   1  2  3
b  16  5  6
c  49  8  9

```

下面的示例对 x 和 y 列进行平方运算：

```python
df.apply(lambda x : np.square(x) if x.name in ['x', 'y'] else x)

    x   y  z
a   1   4  3
b  16  25  6
c  49  64  9


```

下面的示例对第一行 （a 标签所在行）进行平方运算：

```python
df.apply(lambda x : np.square(x) if x.name == 'a' else x, axis=1)

```

默认情况下 `axis=0` 表示按列，`axis=1` 表示按行。

## `apply() `计算日期相减示例

平时我们会经常用到日期的计算，比如要计算两个日期的间隔，比如下面的一组关于 wbs 起止日期的数据：

```python
    wbs   date_from     date_to
  job1  2019-04-01  2019-05-01
  job2  2019-04-07  2019-05-17
  job3  2019-05-16  2019-05-31
  job4  2019-05-20  2019-06-11

```

假定要计算起止日期间隔的天数。比较简单的方法就是两列相减（datetime 类型)：

```python
import pandas as pd
import datetime as dt

wbs = {
    "wbs": ["job1", "job2", "job3", "job4"],
    "date_from": ["2019-04-01", "2019-04-07", "2019-05-16","2019-05-20"],
    "date_to": ["2019-05-01", "2019-05-17", "2019-05-31", "2019-06-11"]
}

df = pd.DataFrame(wbs)
df['elpased'] = df['date_to'].apply(pd.to_datetime) -
					df['date_from'].apply(pd.to_datetime)
```

`apply()` 函数将 `date_from` 和 `date_to` 两列转换成 `datetime` 类型。

print 一下 df:

```

	wbs		date_from	date_to	elpased
0	job1	2019-04-01	2019-05-01	30 days
1	job2	2019-04-07	2019-05-17	40 days
2	job3	2019-05-16	2019-05-31	15 days
3	job4	2019-05-20	2019-06-11	22 days
```

日期间隔已经计算出来，但后面带有一个单位 days，这是因为两个 `datetime` 类型相减，得到的数据类型是 `timedelta64`，如果只要数字，还需要使用 `timedelta` 的 `days` 属性转换一下。

```python
elapsed= df['date_to'].apply(pd.to_datetime) -
    df['date_from'].apply(pd.to_datetime)
df['elpased'] = elapsed.apply(lambda x : x.days)

```

使用 `DataFrame.apply()` 函数也能达到同样的效果，我们需要先定义一个函数 `get_interval_days()` 函数的第一列是一个 `Series` 类型的变量，执行的时候，依次接收 DataFrame 的每一行。

```python
import pandas as pd
import datetime as dt

def get_interval_days(arrLike, start, end):   
    start_date = dt.datetime.strptime(arrLike[start], '%Y-%m-%d')
    end_date = dt.datetime.strptime(arrLike[end], '%Y-%m-%d') 

    return (end_date - start_date).days


wbs = {
    "wbs": ["job1", "job2", "job3", "job4"],
    "date_from": ["2019-04-01", "2019-04-07", "2019-05-16","2019-05-20"],
    "date_to": ["2019-05-01", "2019-05-17", "2019-05-31", "2019-06-11"]
}

df = pd.DataFrame(wbs)
df['elapsed'] = df.apply(
    get_interval_days, axis=1, args=('date_from', 'date_to'))

```

参考：

<a href="https://blog.csdn.net/stone0823/article/details/100008619?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1" blank="">pandas apply() 函数</a> 

<a href="https://www.cjavapy.com/article/303/" blank="">pandas.DataFrame.apply函数方法的使用</a> 