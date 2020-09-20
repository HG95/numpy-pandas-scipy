# Pandas Series.to_frame

Pandas 系列是带有轴标签的一维ndarray。标签不必是唯一的，但必须是可哈希的类型。该对象同时支持基于整数和基于标签的索引，并提供了许多方法来执行涉及索引的操作。

Pandas `Series.to_frame()`函数用于将给定的系列对象转换为 DataFrame 。


用法：` Series.to_frame(name=None)`

**参数：**
**`name`:**传递的名称应替换系列名称(如果有的话)。

**返回：**data_frame：DataFrame



```python
# importing pandas as pd 
import pandas as pd 
  
# Creating the Series 
sr = pd.Series(['New York', 'Chicago', 'Toronto', 'Lisbon', 'Rio', 'Moscow']) 
  
# Create the Datetime Index 
didx = pd.DatetimeIndex(start ='2014-08-01 10:00', freq ='W',  
                     periods = 6, tz = 'Europe/Berlin')  
  
# set the index 
sr.index = didx 
  
# Print the series 
print(sr)
```

输出

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200513091811.png"/>



现在我们将使用`Series.to_frame()`函数将给定的系列对象转换为 DataFrame 

```python
# convert to dataframe 
sr.to_frame()
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200513091916.png"/>



参考

<a href="https://vimsky.com/examples/usage/python-pandas-series-to_frame.html" blank="">Python Pandas Series.to_frame()</a> 