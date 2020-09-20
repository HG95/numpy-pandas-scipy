# Pandas 时间序列—to_period函数

`Series.dt`可用于以datetimelike的形式访问序列的值并返回几个属性。

Pandas `Series.dt.to_period()`函数**以特定频率将给定Series对象的基础数据强制转换为PeriodArray /Index**。

**参数：**

- `freq` ：字符串或偏移量，可选

**返回值：**PeriodArray /索引

**范例1：**

采用`Series.dt.to_period()`函数以每周频率将给定系列对象的基础数据转换为索引。

```python
import pandas as pd 
  
# Creating the Series 
sr = pd.Series(['2012-12-31', '2019-1-1 12:30', '2008-02-2 10:30', 
               '2010-1-1 09:25', '2019-12-31 00:00']) 
  
# Creating the index 
idx = ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5'] 
  
# set the index 
sr.index = idx 
  
# Convert the underlying data to datetime  
sr = pd.to_datetime(sr) 
  
# Print the series 
print(sr)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522163508.png"/>

现在我们将使用`Series.dt.to_period()`函数**以每周频率**将给定系列对象的基础数据转换为索引

```python
# cast to targert frequency 
result = sr.dt.to_period(freq = 'W')  
  
# print the result 
print(result)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522163803.png"/>

正如我们在输出中看到的，`Series.dt.to_period()`功能已成功将数据投射到目标频率。

```python
# cast to targert frequency 
result = sr.dt.to_period(freq = 'M')  
  
# print the result 
print(result)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522163951.png"/>



**范例2：**

采用`Series.dt.to_period()`函数以两年的频率将给定系列对象的基础数据转换为Index。

```python
# Creating the Series 
sr = pd.Series(pd.date_range('2012-12-31 00:00', periods = 5, freq = 'D')) 
  
# Creating the index 
idx = ['Day 1', 'Day 2', 'Day 3', 'Day 4', 'Day 5'] 
  
# set the index 
sr.index = idx 
  
# Print the series 
print(sr)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522164232.png"/>

现在我们将使用`Series.dt.to_period()`函数以两年的频率将给定系列对象的基础数据转换为Index。

```python
# cast to targert frequency 
result = sr.dt.to_period(freq = '2Y')  
  
# print the result 
print(result)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200522164407.png"/>



参考

[Python Pandas Series.dt.to_period用法及代码示例](https://vimsky.com/examples/usage/python-pandas-series-dt-to_period.html) 

