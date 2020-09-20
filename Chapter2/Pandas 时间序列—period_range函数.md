# Pandas 时间序列—period_range函数



```python
pd.period_range(start=None, 
                end=None, 
                periods=None, 
                freq='D', 
                name=None)
#时间段范围返回PeriodIndex
```

参数

```
start=None : #string or period-like,期间开始
end=None : #string or period-like,期间结束
periods =None: #integer,要生成的周期数
freq='D' : #string or DateOffset
name=None : str,# 生成PeriodIndex的名称
```

生成日期序列

主要提供`pd.data_range()`和`pd.period_range()`两个方法，给定参数有起始时间、结束时间、生成时期的数目及时间频率（freq='M’月，'D’天，‘W’，周，'Y’年）等。

两种主要区别在于`pd.date_range()` 生成的是`DatetimeIndex` 格式的日期序列；`pd.period_range()` 生成的是`PeriodIndex`格式的日期序列。
以下通过生成月时间序列和周时间序列来对比下：



```python
date_rng = pd.date_range('2019-01-01', freq='M', periods=12)
print(f'month date_range()：\n{date_rng}')
"""
date_range()：
DatetimeIndex(['2019-01-31', '2019-02-28', '2019-03-31', '2019-04-30',
               '2019-05-31', '2019-06-30', '2019-07-31', '2019-08-31',
               '2019-09-30', '2019-10-31', '2019-11-30', '2019-12-31'],
              dtype='datetime64[ns]', freq='M')
"""

period_rng = pd.period_range('2019/01/01', freq='M', periods=12)
print(f'month period_range()：\n{period_rng}')
"""
period_range()：
PeriodIndex(['2019-01', '2019-02', '2019-03', '2019-04', '2019-05', '2019-06',
             '2019-07', '2019-08', '2019-09', '2019-10', '2019-11', '2019-12'],
            dtype='period[M]', freq='M')
"""

date_rng = pd.date_range('2019-01-01', freq='W-SUN', periods=12)
print(f'week date_range()：\n{date_rng}')
"""
week date_range()：
DatetimeIndex(['2019-01-06', '2019-01-13', '2019-01-20', '2019-01-27',
               '2019-02-03', '2019-02-10', '2019-02-17', '2019-02-24',
               '2019-03-03', '2019-03-10', '2019-03-17', '2019-03-24'],
              dtype='datetime64[ns]', freq='W-SUN')
"""

period_rng=pd.period_range('2019-01-01',freq='W-SUN',periods=12)
print(f'week period_range()：\n{period_rng}')
"""
week period_range()：
PeriodIndex(['2018-12-31/2019-01-06', '2019-01-07/2019-01-13',
             '2019-01-14/2019-01-20', '2019-01-21/2019-01-27',
             '2019-01-28/2019-02-03', '2019-02-04/2019-02-10',
             '2019-02-11/2019-02-17', '2019-02-18/2019-02-24',
             '2019-02-25/2019-03-03', '2019-03-04/2019-03-10',
             '2019-03-11/2019-03-17', '2019-03-18/2019-03-24'],
            dtype='period[W-SUN]', freq='W-SUN')
"""
date_rng = pd.date_range('2019-01-01 00:00:00', freq='H', periods=12)
print(f'hour date_range()：\n{date_rng}')
"""
hour date_range()：
DatetimeIndex(['2019-01-01 00:00:00', '2019-01-01 01:00:00',
               '2019-01-01 02:00:00', '2019-01-01 03:00:00',
               '2019-01-01 04:00:00', '2019-01-01 05:00:00',
               '2019-01-01 06:00:00', '2019-01-01 07:00:00',
               '2019-01-01 08:00:00', '2019-01-01 09:00:00',
               '2019-01-01 10:00:00', '2019-01-01 11:00:00'],
              dtype='datetime64[ns]', freq='H')
"""
period_rng=pd.period_range('2019-01-01 00:00:00',freq='H',periods=12)
print(f'hour period_range()：\n{period_rng}')
"""
hour period_range()：
PeriodIndex(['2019-01-01 00:00', '2019-01-01 01:00', '2019-01-01 02:00',
             '2019-01-01 03:00', '2019-01-01 04:00', '2019-01-01 05:00',
             '2019-01-01 06:00', '2019-01-01 07:00', '2019-01-01 08:00',
             '2019-01-01 09:00', '2019-01-01 10:00', '2019-01-01 11:00'],
            dtype='period[H]', freq='H')
"""
```

