# Pandas 统计函数corr

相关系数(correlation coefficients)

计算列与列之间的相关系数 (不包括NA/null)，返回相关系数矩阵

```python
DataFrame.corr( method='pearson', min_periods=1) → ’DataFrame’
```

参数：

- `method`:{‘pearson’, ‘kendall’, ‘spearman’} or callable
  - ` pearson`：标准相关系数
  - `kendall`：Kendall Tau相关系数
  -  `spearman`：Spearman等级相关
  - `callable`：可输入两个1d ndarray来调用

返回值：`DataFrame`

## Examples

```python
allDf = pd.DataFrame({
    'x':[0,1,2,4,7,10],
    'y':[0,3,2,4,5,7],
    's':[0,1,2,3,4,5],
    'c':[5,4,3,2,1,0]
},index = ['p1','p2','p3','p4','p5','p6'])

allDf
```

结果：

```
	x	y	s	c
p1	0	0	0	5
p2	1	3	1	4
p3	2	2	2	3
p4	4	4	3	2
p5	7	5	4	1
p6	10	7	5	0
```

```python
allDf.corr()
```

结果：

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200712140833.png" alt="image-20200711145148964" style="zoom: 67%;" /></center>

```python
allDf.corr()['x']
```

<center><img src=".\img\image-20200711145222334.png" alt="image-20200711145222334" style="zoom:67%;" /></center>



## 参考

- <a href="https://blog.csdn.net/dss_dssssd/article/details/82811300" target="_blank">pandas 统计函数corr</a>
- <a href="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html?highlight=corr" target="_blank">pandas.DataFrame.corr</a> 