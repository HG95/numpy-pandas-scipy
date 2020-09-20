# Pandas 字符数据的处理方法

在商业数据表中，经常需要处理字符型的数据，而 pandas 中的 Series.str属性就有几下几十种方法可以处理字符串数据。

## `Series.str.extract()`

`str.extract()`，可用正则从字符数据中抽取匹配的数据，**注意要加上括号，** **只返回第一个匹配的数据**（要将自己要提取的内容加上括号，括号外的不提取）

注意，正则表达式中必须有分组，只是返回分组中的数据，如果给分组取了名称，则该名称就是返回结果中的字段名。

```python
Series.str.extract(pat, flags=0, expand=None)
```

参数:

- `pat` : 字符串或正则表达式

- `flags` : 整型,

- `expand` : 布尔型,是否返回DataFrame

  当字符串中含有多个要提取的变量时，`expand=True` 会将其分割为多列

  Returns:
  数据框dataframe/索引index

```python
for i in df:
    df['Title']=df_raw['Name'].str.extract('([A-Za-z]+)\.', expand=False)
```



## `str.extractall()`

```python
Series.str.extractall(pat, flags=0)
```

返回所有匹配的字符
参数:

- `pat `: 字符串或正则表达式
- `flags` : 整型
  返回值:

## `Series.str.cat()`

```python
Series.str.cat(others=None, sep=None, na_rep=None)
```

> 用给定的字符链接序列或索引中的字符串
> 返回：合并后的序列
> 注：当na_rep为None，序列中的nan值将被忽略，如果指定，将用该字符代替

```python
>>> df.index.str.cat(['1','2','3'],sep = ',')
Index(['f,1', 'g,2', 'h,3'], dtype='object')
>>> df.index.str.cat([['1','2','3'],['4','5','6']],sep='*')
Index(['f*1*4', 'g*2*5', 'h*3*6'], dtype='object')
>>> df.index.str.cat(sep='*')
'f*g*h'
>>> 
```



## `Series.str.get() `

获取指定位置的字符串

## `Series.str.contains() `

是否包含表达式

```python
Series.str.contains(pat, case=True, flags=0, na=nan, regex=True)
```

判断给定的字符串或者正则表达式是否在序列或者索引中
**返回：bool** 

```python
>>> df
   a  b hh
f  1  4  d
g  2  5  f
h  3  6  g
>>> df['hh'].str.contains('f')
f    False
g     True
h    False
Name: hh, dtype: bool
```

参数 `na` 当数据中有空值的时候 处理的策略

```python
mapping = {'liucixin': '刘慈欣|大刘', 'guofan': '郭帆', 'quchuxiao': '屈楚萧|刘启|户口', 'wujing': '吴京|刘培强',
           'liguangjie': '李光洁|王磊', 'wumengda': '吴孟达|达叔|韩子昂', 'zhaojinmai': '赵今麦|韩朵朵'}
for key, value in mapping.items():
    data[key] = data['content'].str.contains(value,na=False)
```

**处理后得到结果 全部为 bool 类型的值， 不包含 NA/   等空值**





## `Series.str.count()`

```python
Series.str.count(pat, flags=0, **kwargs)
```

计算pat在序列或者索引字符串中出现的次数

```python
>>> df['count']=['hello','hello','hel']
>>> df
   a  b hh  count
f  1  4  d  hello
g  2  5  f  hello
h  3  6  g    hel
>>> df['count'].str.count('hel')
f    1
g    1
h    1
Name: count, dtype: int64
>>> df['count'].str.count('l')
f    2
g    2
h    1
Name: count, dtype: int64
```

## `Series.str.decode()`

```python
Series.str.decode(encoding, errors=’strict’)
```

对指定的编码方式进行解码（‘utf-8’,'gbk'等等）

## `Series.str.endswith()`

```python
Series.str.endswith(pat, na=nan)
```

判断是否已给定的 pat 结尾

## 其他

## `split() `切分字符串

`str.split()`有三个参数：

第一个参数就是引号里的内容：就是分列的依据，可以是空格，符号，字符串等等。

第二个参数就是前面用到的`expand=True`，这个参数直接将分列后的结果转换成DataFrame。

第三个参数的`n=数字`就是限制分列的**次数** 。

**就是当用于分列的依据符号在有多个的话需要指定分列的次数（不指定的话就会根据符号有几个分列几次）。**

```python
data.auth_capital.sample(5)
"""
411               注册资本：100 万元
735          注册资本：53760 万元人民币
607         注册资本：1476.92万元人民币
464         注册资本：22.3464万元人民币
12      注册资本：430077.1898万人民币元
"""
auth_capital = data['auth_capital'].str.split('：', expand = True)
auth_capital.sample(5)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514103620.png"/>



`join() `对每个字符都用给点的字符串拼接起来，不常用

`replace() `替换

`repeat()` 重复

`pad()` 左右补齐

```python
>>> s.str.pad(10, fillchar="?")
0 ?????a_b_c
1 ?????c_d_e
2 NaN
3 ?????f_g_h
dtype: object
>>>
>>> s.str.pad(10, side="right", fillchar="?")
0 a_b_c?????
1 c_d_e?????
2 NaN
3 f_g_h?????
dtype: object
```

`slice()` 按给定的开始结束位置切割字符串

```python
>>> s.str.slice(1,3)
0 _b
1 _d
2 NaN
3 _g
dtype: object
```

`slice_replace() `使用给定的字符串，替换指定的位置的字符

```python
>>> s.str.slice_replace(1, 3, "?")
0 a?_c
1 c?_e
2 NaN
3 f?_h
dtype: object
>>> s.str.slice_replace(1, 3, "??")
0 a??_c
1 c??_e
2 NaN
3 f??_h
dtype: object
```

## `findall() `

查找所有符合正则表达式的字符，以数组形式返回

```python
>>> s.str.findall("[a-z]");
0 [a, b, c]
1 [c, d, e]
2 NaN
3 [f, g, h]
dtype: object
```

## `partition() `

把字符串数组切割称为DataFrame，注意切割只是切割称为三部分，分隔符前，分隔符，分隔符后

## `rpartition() `

从右切起

## `lower() `

全部小写

## `upper() `

全部大写

参考

<a href="https://zhuanlan.zhihu.com/p/30894133" blank="" >Pandas之Series.str列内置的方法</a> 