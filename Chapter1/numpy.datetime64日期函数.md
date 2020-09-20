# numpy.datetime64()日期函数

## Basic Datetimes 

创建数据时间的最基本的方法是使用ISO 8601日期或日期时间格式的字符串。内部存储单元是从字符串的形式自动选择的，可以是date unit或time unit。

日期单位是年（‘Y’），月（‘M’），星期（‘W’）和日（‘D’），而时间单位是小时（h），秒（‘s’），毫秒（‘ms’）和一些附加的基于秒前缀的单位。

## **简单的ISO日期**

```python
>>> np.datetime64('2005-02-25')
numpy.datetime64('2005-02-25')

str(np.datetime64('2005-02-25'))
#'2005-02-25'

```

## **使用月份为单位**

```python
>>> np.datetime64('2005-02')
numpy.datetime64('2005-02')

```

**仅指定月份，但强制使用“天”单位：**

```python
>>> np.datetime64('2005-02', 'D')
numpy.datetime64('2005-02-01')

```

**从字符串创建数据集的数组时，仍然可以使用带有通用单位的日期时间类型从输入中自动选择单位。**

```python
>>> np.array(['2007-07-13', '2006-01-13', '2010-08-13'], dtype='datetime64')
array(['2007-07-13', '2006-01-13', '2010-08-13'], dtype='datetime64[D]')

```

## **生成日期范围**

**datetime类型适用于许多常见的NumPy函数，例如`arange`可用于生成日期范围。**

所有日期一个月：
指定格式`dtype=datetime64[D]`  天

```python
Z = np.arange('2016-07', '2016-08', dtype='datetime64[D]')

'''
array(['2016-07-01', '2016-07-02', '2016-07-03', '2016-07-04',
       '2016-07-05', '2016-07-06', '2016-07-07', '2016-07-08',
       '2016-07-09', '2016-07-10', '2016-07-11', '2016-07-12',
       '2016-07-13', '2016-07-14', '2016-07-15', '2016-07-16',
       '2016-07-17', '2016-07-18', '2016-07-19', '2016-07-20',
       '2016-07-21', '2016-07-22', '2016-07-23', '2016-07-24',
       '2016-07-25', '2016-07-26', '2016-07-27', '2016-07-28',
       '2016-07-29', '2016-07-30', '2016-07-31'], dtype='datetime64[D]')
'''


```

## 日期和时间的增量算法 `timedelta64`

NumPy 允许减去两个日期时间值，一个产生具有时间单位的数字的操作。由于 NumPy 在其核心中没有物理量系统，因此创建了`timedelta64`数据类型以补充`datetime64。`
`Datetimes` 和`Timedeltas` 一起工作，为简单的日期时间计算提供方法。

```python
>>> np.datetime64('2009-01-01') - np.datetime64('2008-01-01')
#numpy.timedelta64(366,'D')

str(np.datetime64('2009-01-01') - np.datetime64('2008-01-01'))
'366 days'

str(np.datetime64('2009-01-01') - np.datetime64('2008-01-01')).split(" ")[0]
#'366'

```

## np.busday_count()

要查找datetime64日期的指定范围内有多少有效天数，请使用[`busday_count`](http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.busday_count.html#numpy.busday_count)：

```python
>>> np.busday_count(np.datetime64('2011-07-11'), np.datetime64('2011-07-18'))
5
>>> np.busday_count(np.datetime64('2011-07-18'), np.datetime64('2011-07-11'))
-5
```

如果你有一个datetime64 day值的数组，并且你想要一个有多少是有效日期的计数，你可以这样做：

```python
>>> a = np.arange(np.datetime64('2011-07-11'), np.datetime64('2011-07-18'))
>>> np.count_nonzero(np.is_busday(a))
5
```

## 参考：

<a href="http://doc.codingdict.com/NumPy_v111/reference/arrays.datetime.html" blank="" >Datetimes and Timedeltas</a> 

