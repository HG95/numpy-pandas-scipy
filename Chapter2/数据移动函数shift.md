# 数据移动函数shift

shift函数是对数据进行移动的操作

###### pandas.DataFrame.shift

```python
DataFrame.shift(periods=1, freq=None, axis=0, fill_value=None)
```

参数：

- `period`：表示移动的幅度，可以是正数，也可以是负数，默认值是1,1就表示移动一次，注意这里移动的都是数据，而索引是不移动的，移动之后没有对应值的，就赋值为NaN。
- `freq`： DateOffset, timedelta, or time rule string，可选参数，默认值为None，只适用于时间序列，如果这个参数存在，那么会按照参数值移动时间索引，而数据值没有发生变化。
- `axis`： 轴向。 **{0 or ‘index’, 1 or ‘columns’, None}, default None** 表示移动的方向，如果是0或者’index’表示上下移动，如果是1或者’columns’，则会左右移动。
- `fill_value` : object, optional  数据移动后缺失值填补的方法



###### **Examples**

- 设定 period 与 axis

```python
df = pd.DataFrame(np.arange(16).reshape(4,4),columns=['AA','BB','CC','DD'],index =['a','b','c','d'])

df
Out[14]: 
   AA  BB  CC  DD
a   0   1   2   3
b   4   5   6   7
c   8   9  10  11
d  12  13  14  15

#当period为正时，默认是axis = 0轴的设定，向下移动
df.shift(2)
Out[15]: 
    AA   BB   CC   DD
a  NaN  NaN  NaN  NaN
b  NaN  NaN  NaN  NaN
c  0.0  1.0  2.0  3.0
d  4.0  5.0  6.0  7.0

#当axis=1，沿水平方向进行移动，正数向右移，负数向左移
df.shift(2,axis = 1)
Out[16]: 
   AA  BB    CC    DD
a NaN NaN   0.0   1.0
b NaN NaN   4.0   5.0
c NaN NaN   8.0   9.0
d NaN NaN  12.0  13.0

#当period为负时，默认是axis = 0轴的设定，向上移动
df.shift(-1)
Out[17]: 
     AA    BB    CC    DD
a   4.0   5.0   6.0   7.0
b   8.0   9.0  10.0  11.0
c  12.0  13.0  14.0  15.0
d   NaN   NaN   NaN   NaN
```

- freq 参数实例

```python
df = pd.DataFrame(np.arange(16).reshape(4,4)
                  ,columns=['AA','BB','CC','DD']
                  ,index =pd.date_range('6/1/2012','6/4/2012'))

df
Out[38]: 
            AA  BB  CC  DD
2012-06-01   0   1   2   3
2012-06-02   4   5   6   7
2012-06-03   8   9  10  11
2012-06-04  12  13  14  15

df.shift(freq=datetime.timedelta(1))
Out[39]: 
            AA  BB  CC  DD
2012-06-02   0   1   2   3
2012-06-03   4   5   6   7
2012-06-04   8   9  10  11
2012-06-05  12  13  14  15

df.shift(freq=datetime.timedelta(-2))
Out[40]: 
            AA  BB  CC  DD
2012-05-30   0   1   2   3
2012-05-31   4   5   6   7
2012-06-01   8   9  10  11
2012-06-02  12  13  14  15
```

- fill_value 参数

```python
df = pd.DataFrame({"Col1": [10, 20, 15, 30, 45],
                   "Col2": [13, 23, 18, 33, 48],
                   "Col3": [17, 27, 22, 37, 52]
                   ,index=pd.date_range("2020-01-01", "2020-01-05"))
df
            Col1  Col2  Col3
2020-01-01    10    13    17
2020-01-02    20    23    27
2020-01-03    15    18    22
2020-01-04    30    33    37
2020-01-05    45    48    52
                   
                   
df.shift(periods=3, fill_value=0)
            Col1  Col2  Col3
2020-01-01     0     0     0
2020-01-02     0     0     0
2020-01-03     0     0     0
2020-01-04    10    13    17
2020-01-05    20    23    27
                                   
```

- `periods 与 freq` 同时使用：

```python
df = pd.DataFrame({"Col1": [10, 20, 15, 30, 45],
                   "Col2": [13, 23, 18, 33, 48],
                   "Col3": [17, 27, 22, 37, 52]
                   ,index=pd.date_range("2020-01-01", "2020-01-05"))
df
            Col1  Col2  Col3
2020-01-01    10    13    17
2020-01-02    20    23    27
2020-01-03    15    18    22
2020-01-04    30    33    37
2020-01-05    45    48    52
                   
df.shift(periods=3, freq="D")
            Col1  Col2  Col3
2020-01-04    10    13    17
2020-01-05    20    23    27
2020-01-06    15    18    22
2020-01-07    30    33    37
2020-01-08    45    48    52                   
```

