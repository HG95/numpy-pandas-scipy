# Pandas resample方法详解

Pandas中的 `resample`，重新采样，是对原样本重新处理的一个方法，是一个对常规时间序列数据重新采样和频率转换的便捷的方法。

```python
DataFrame.resample(rule, 
                   how=None, 
                   axis=0, 
                   fill_method=None, 
                   closed=None, 
                   label=None, 
                   convention='start',
                   kind=None, 
                   loffset=None, 
                   limit=None, 
                   base=0)
```

- `rule` : string
  偏移量表示目标字符串或对象转换

- `axis` : int, optional, default 0

- ` closed `: {‘right’, ‘left’}
  哪一个方向的间隔是关闭的

- `label` : {‘right’, ‘left’}
  Which bin edge label to label bucket with

- `convention` : {‘start’, ‘end’, ‘s’, ‘e’}

- `loffset` : timedelta
  调整重新取样时间标签

- `base` : int, default 0
  频率均匀细分1天,“起源”的聚合的间隔。例如,对于“5分钟”频率,基地可能范围从0到4。默认值为0


首先创建一个Series，采样频率为一分钟。

```python
>>> index = pd.date_range('1/1/2000', periods=9, freq='T')
>>> series = pd.Series(range(9), index=index)
>>> series
2000-01-01 00:00:00    0
2000-01-01 00:01:00    1
2000-01-01 00:02:00    2
2000-01-01 00:03:00    3
2000-01-01 00:04:00    4
2000-01-01 00:05:00    5
2000-01-01 00:06:00    6
2000-01-01 00:07:00    7
2000-01-01 00:08:00    8
Freq: T, dtype: int64

```

**降低采样频率为三分钟**

```python
>>> series.resample('3T').sum()
2000-01-01 00:00:00     3
2000-01-01 00:03:00    12
2000-01-01 00:06:00    21
Freq: 3T, dtype: int64
```

降低采样频率为三分钟，但是每个标签使用right来代替left。请注意，bucket中值的用作标签。

```python
>>> series.resample('3T', label='right').sum()
2000-01-01 00:03:00     3
2000-01-01 00:06:00    12
2000-01-01 00:09:00    21
Freq: 3T, dtype: int64

```

降低采样频率为三分钟，但是关闭right区间。

```python
>>> series.resample('3T', label='right', closed='right').sum()
2000-01-01 00:00:00     0
2000-01-01 00:03:00     6
2000-01-01 00:06:00    15
2000-01-01 00:09:00    15
Freq: 3T, dtype: int64
```



## 示例

看一个dataframe，index是时间，columns 是 price 和 volume：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200518091205.png"/>

该dataframe的时间分布式不均匀的，然而很多统计分析建模都是需要时间均匀间隔的数据的，好在 pandas 为我们提供了 resample 这一函数可以解决这一问题。比如如果我们想要洗成 1min 频率的数据我们就可以这样做：

```python
df = df.resample('60S').last()
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200518091300.png"/>

可以看到经过 resample 函数的重新抽样，新的dataframe已经变成了等间距的分钟级别数据。其中 `last()` 表示使用每个分钟段区间内的最后一个数据作为该分钟最终显示的数据，如果该分钟内没有任何数据则会显示NaN，比如2014-12-07 00:02:00。除了last之外，还有`first`，`mean`，`sum` 等等。



但是，从新的 dataframe 中我们还是可以观察出两个问题，第一，原 dataframe 的第一个记录是00:00:07，然而这个数据却被自动附到了新dataframe中00:00:00的index上。而事实上在00:00:00时刻，我们并不知道00:00:07发生了什么。第二，对于volume而言一般不应该使用last而应该是用sum函数，代表了这个时间段内的总的交易量，会更有意义。



重新写我们的resample函数如下：

```python
price = df['price].resample('60S', label = 'right').last()
volume = df['price].resample('60S', label = 'right').sum()
df = pd.concat([price, volume], axis = 1)
```

在这段代码里，首先我们通过设置label的参数去解决第一个问题。在resample函数里，label默认值是left，也就是把一个区间内的数据的计算结果都附到区间左侧端点上，而我们想要的则是相反的情况，也就是label = right。其次，我们通过将price和volume分开处理，price使用last，volume则使用sum函数，达到了更合理的处理效果。最后，我们用concat函数将两个Series合并，就得到了如下结果：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200518091649.png"/>

最后，我们还可以利用apply和lambda函数计算每一分钟的VWAP，也就是每分钟交易量加权的价格，代码如下：



```python
df.resample('60S', label = 'right').apply(lambda x:np.average(x['price']
            ,weights = x['volume']) if sum(x['volume']) != 0 else 
             np.average(x['price']))[['price']]
```

可以看到，我们用到了numpy里的average函数帮我们计算weighted average，其中weights就是每个时间区段内的所有volume数据。后面我们为了避免错误加了一个判读：如果这个区间内volume加和等于0，也即没有数据我们就直接返回价格平均值（实际上也只会返回NaN）。最后由于resample函数返回的dataframe中price和volume都被附上了新的VWAP值，所以我们通过下标只选择price这一列数据，多用一个中括号是为了索引后得到的仍旧是一个dataframe，打印比较美观。

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200518091944.png"/>



## 参考

1. <a href="https://zhuanlan.zhihu.com/p/35016415" blank="">【金融数据处理Tricks】1. Resample</a> 
2. <a href="https://blog.csdn.net/wangshuang1631/article/details/52314944" blank="">Pandas中resample方法详解</a>  