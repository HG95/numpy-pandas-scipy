# Pandas 分位数quantile

```python
DataFrame.quantile(q=0.5, 
                   axis=0, 
                   numeric_only=True, 
                   interpolation='linear')
```

参数：

- **q** ：**float or array-like, default 0.5 (50%** **quantile**)

- **axis** ：{0, 1, ‘index’, ‘columns’}, default 0

  Equals 0 or ‘index’ for row-wise, 1 or ‘columns’ for column-wise.

- **numeric_only**： bool, default True

  If False, the quantile of datetime and timedelta data will be computed as well.

- **interpolation**：（插值方法） : {‘linear’, ‘lower’, ‘higher’, ‘midpoint’, ‘nearest’} 

  当选中的分为点位于两个数数据点 i and j 之间时:  

    linear: i + (j - i) * fraction, fraction由计算得到的pos的小数部分（可以通过下面一个例子来理解这个fraction）；    

  lower: i.    

  nearest: i or j whichever is nearest.    

  midpoint: (i + j) / 2.



返回值：

- **Series or DataFrame**

  If `q` is an array, a DataFrame will be returned where the

  index is `q`, the columns are the columns of self, and the values are the quantiles.

  If `q` is a float, a Series will be returned where the

  index is the columns of self and the values are the quantiles.

## 统计学上的四分为函数

原则上p是可以取0到1之间的任意值的。但是有一个四分位数是p分位数中较为有名的。

所谓四分位数；即把数值由小到大排列并分成四等份，处于三个分割点位置的数值就是四分位数。

- **第1四分位数 (Q1)**，又称“较小四分位数”，等于该样本中所有数值由小到大排列后第25%的数字。
- **第2四分位数 (Q2)**，又称“中位数”，等于该样本中所有数值由小到大排列后第50%的数字。
- **第3四分位数 (Q3)**，又称“较大四分位数”，等于该样本中所有数值由小到大排列后第75%的数字。

第3四分位数与第1四分位数的差距又称四分位距（InterQuartile Range,IQR）

## 计算方法与举例

#### **五大因“数”**

我们一组序列数为例：12，15，17，19，20，23，25，28，30，33，34，35，36，37讲解这五大因“数”

![img](http://upload-images.jianshu.io/upload_images/7897295-8e68dec174a0e8eb?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**1、下四分位数Q1**

（1）确定四分位数的位置。Qi所在位置=i*（n+1）/4，其中i=1，2，3。n表示序列中包含的项数。

（2）根据位置，计算相应的四分位数。

例中：

Q1所在的位置=（14+1）/4=3.75，

Q1=0.25×第三项+0.75×第四项=0.25×17+0.75×19=18.5；

**2、中位数（第二个四分位数）Q2**

中位数，即一组数由小到大排列处于中间位置的数。若序列数为偶数个，该组的中位数为中间两个数的平均数。

例中：

Q2所在的位置=2*（14+1）/4=7.5，

Q2=0.5×第七项+0.5×第八项=0.5×25+0.5×28=26.5

**3、上四分位数Q3**

计算方法同下四分位数。

例中：

Q3所在的位置=3*（14+1）/4=11.25，

Q3=0.75×第十一项+0.25×第十二项=0.75×34+0.25×35=34.25。

**4、上限**

上限是非异常范围内的最大值。

首先要知道什么是四分位距如何计算的？

四分位距IQR=Q3-Q1，那么上限=Q3+1.5IQR

**5、下限**

下限是非异常范围内的最小值。

下限=Q1-1.5IQR

为了更一般化，在计算的过程中，我们考虑p分位。当p=0.25 0.5 0.75 时，就是在计算四分位数。

首先确定p分位数的位置（有两种方法）：

> 方法1 pos = (n+1)*p
> 方法2 pos = 1+(n-1)*p

pandas 中使用的是方法2确定的。



```python
df = pd.DataFrame(np.array([[1, 1], [2, 10], [3, 100], [4, 100]]),
                  columns=['a', 'b'])

df
	a	b
0	1	1
1	2	10
2	3	100
3	4	100

df.quantile(.1)
a    1.3
b    3.7
Name: 0.1, dtype: float64
        
df.quantile([.1, .5])
       a     b
0.1  1.3   3.7
0.5  2.5  55.0
```

```python
data.price.quantile([0.25,0.5,0.75])

//输出
0.25  42812.25
0.50  57473.00
0.75  76099.75
```







参考：

- <a href="https://blog.csdn.net/clairliu/article/details/79217546" target="_blank">搞懂箱形图分析，快速识别异常值！</a>

