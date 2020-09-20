# Pandas pd.cut()函数

将数据进行离散化

```python
pandas.cut(x,
           bins,
           right=True,
           labels=None,
           retbins=False,
           precision=3,
           include_lowest=False
          )
```

参数

- `x`   : 进行划分的一维数组

-  `bins `: 
  - 整数---将 x 划分为多少个等间距的区间
  - 序列—将 x 划分在指定的序列中，若不在该序列中，则是NaN
-  `right` : 是否包含右端点
-  ` labels` : 是否用标记来代替返回的bins
- ` precision`: 精度
- `include_lowest`: 是否包含左端点

返回值:

   如果 `retbins = False` 则返回x中每个值对应的bin的列表，否者则返回x中每个值对应的bin的列表和对应的bins



`pd.cut(` 的作用，有点类似给成绩设定优良中差，比如：0-59分为差，60-70分为中，71-80分为优秀等等，在pandas中，也提供了这样一个方法来处理这些事儿。

```python
import numpy as np
import pandas as pd

np.random.seed(666)
score_list = np.random.randint(25,100,20) 
```

```python
score_list

array([27, 70, 55, 87, 95, 98, 55, 61, 86, 76, 85, 53, 39, 88, 41, 71, 64,
       94, 38, 94])
```

```python
# 指定多个区间
bins = [0, 59, 70, 80, 100]
score_cut = pd.cut(score_list, bins)
```

```python
type(score_cut)
# pandas.core.arrays.categorical.Categorical
```

```python
score_cut

[(0, 59], (59, 70], (0, 59], (80, 100], (80, 100], ..., (70, 80], (59, 70], (80, 100], (0, 59], (80, 100]]
Length: 20
Categories (4, interval[int64]): [(0, 59] < (59, 70] < (70, 80] < (80, 100]]
```

```python
# 统计每个区间的人数
pd.value_counts(score_cut)

(80, 100]    8
(0, 59]      7
(59, 70]     3
(70, 80]     2
dtype: int64
```



```python
df = pd.DataFrame()
df['score'] = score_list
df['student'] = [pd.util.testing.rands(3) for i in range(len(score_list))]
df
```

```python
	score	student
0	27	1ul
1	70	yuK
2	55	WWK
3	87	EU6
4	95	Vqn
5	98	KAf
6	55	QNT
7	61	HaE
8	86	aBo
9	76	MMa
10	85	Ctc
11	53	5BI
12	39	wBp
13	88	WMB
14	41	q5t
15	71	MjZ
16	64	nTc
17	94	Kyx
18	38	Rlh
19	94	2uV
```

```python
# 使用cut方法进行分箱
pd.cut(df['score'], bins)
```

```
0       (0, 59]
1      (59, 70]
2       (0, 59]
3     (80, 100]
4     (80, 100]
5     (80, 100]
6       (0, 59]
7      (59, 70]
8     (80, 100]
9      (70, 80]
10    (80, 100]
11      (0, 59]
12      (0, 59]
13    (80, 100]
14      (0, 59]
15     (70, 80]
16     (59, 70]
17    (80, 100]
18      (0, 59]
19    (80, 100]
Name: score, dtype: category
Categories (4, interval[int64]): [(0, 59] < (59, 70] < (70, 80] < (80, 100]]
```

```python
df['Categories'] = pd.cut(df['score'], bins)
df
```

```
	score	student	Categories
0	27	1ul	(0, 59]
1	70	yuK	(59, 70]
2	55	WWK	(0, 59]
3	87	EU6	(80, 100]
4	95	Vqn	(80, 100]
5	98	KAf	(80, 100]
6	55	QNT	(0, 59]
7	61	HaE	(59, 70]
8	86	aBo	(80, 100]
9	76	MMa	(70, 80]
10	85	Ctc	(80, 100]
11	53	5BI	(0, 59]
12	39	wBp	(0, 59]
13	88	WMB	(80, 100]
14	41	q5t	(0, 59]
15	71	MjZ	(70, 80]
16	64	nTc	(59, 70]
17	94	Kyx	(80, 100]
18	38	Rlh	(0, 59]
19	94	2uV	(80, 100]
```

```python
# 但是这样的方法不是很适合阅读，可以使用cut方法中的label参数
# 为每个区间指定一个label
df['Categories'] = pd.cut(df['score'], bins, labels=[
                          'low', 'middle', 'good', 'perfect'])

df
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200507155624.png"/>

## 参考：

<a href="https://blog.csdn.net/missyougoon/article/details/83986511" blank="">pandas中pd.cut()的功能和作用</a> 