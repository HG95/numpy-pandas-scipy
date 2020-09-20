# Pandas 时间序列—to_datetime函数



`pandas.to_datetime()`，它是pandas库的一个方法， 这个方法的实用性在于，当需要批量处理时间数据时，无疑是最好用的。

主要几个参数

```python
pandas.to_datetime(	arg,
					errors ='raise',
					utc = None,
					format = None,
					unit = None )
```

- `format` 格式化显示时间的格式。如 "%Y-%m-%d",.....

- `units` 默认值为‘ns’，则将会精确到微妙，‘s'为秒。

- `errors`  三种取值，‘ignore’, ‘raise’, ‘coerce’，默认为raise。

  'raise'，则无效的解析将引发异常

  'coerce'，那么无效解析将被设置为NaT

  'ignore'，那么无效的解析将返回输入值



```
1、
df = pd.DataFrame({'year': [2015, 2016],
                       'month': [2, 3],
                       'day': [4, 5]})
pd.to_datetime(df)
#0   2015-02-04
#1   2016-03-05
#dtype: datetime64[ns]
#可以看到将字典形式时间转换为可读时间
 
2、
pd.to_datetime('13000101', format='%Y%m%d', errors='ignore')
#datetime.datetime(1300, 1, 1, 0, 0)
 
pd.to_datetime('13000101', format='%Y%m%d', errors='coerce')
#NaT
#如果日期不符合时间戳限制，则errors ='ignore'将返回原始输入，而不会报错。
#errors='coerce'将强制超出NaT的日期，返回NaT。
```

然而实际中遇到的可能是这样的数据：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522155305.png"/>

> 通过pandas.read_csv()或者pandas.read_excel()读取文件过后，得到的数据列对应的类型是“object”，这样没法对时间数据处理，可以用过`pd.to_datetime` 将该列数据转换为时间类型，即`datetime` 。

```python
data.dtypes
# object
 
data= pd.to_datetime(data)
data.dtypes
# datetime64[ns]
```

转换过后就可以对这些时间数据操作了，可以相减求时间差，计算相差的秒数和天数，调用的方法和`datetime`库的方法一致，分别是 `data.dt.days() `、`data.dt.seconds()` 、`data.dt.total_seconds()`



参考：

[https://www.pypandas.cn/docs/user_guide/timeseries.html#%E7%BA%B5%E8%A7%88](https://www.pypandas.cn/docs/user_guide/timeseries.html#纵览) 

