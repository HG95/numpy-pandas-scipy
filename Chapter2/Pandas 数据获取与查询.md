# Pandas 数据获取与查询 

数据的查看

```python
import numpy as np
import pandas as pd
from pandas import Sereis, DataFrame

ser = Series(np.arange(3.))

data = DataFrame(np.arange(16).reshape(4,4),index=list('abcd'),columns=list('wxyz'))

data['w']  #选择表格中的'w'列，使用类字典属性,返回的是Series类型

data.w    #选择表格中的'w'列，使用点属性,返回的是Series类型

data[['w']]  #选择表格中的'w'列，返回的是DataFrame类型

data[['w','z']]  #选择表格中的'w'、'z'列

data[0:2]  #返回第1行到第2行的所有行，前闭后开，包括前不包括后

data[1:2]  #返回第2行，从0计，返回的是单行，通过有前后值的索引形式，
       #如果采用data[1]则报错

data.ix[1:2] #返回第2行的第三种方法，返回的是DataFrame，跟data[1:2]同

data['a':'b']  #利用index值进行切片，返回的是**前闭后闭**的DataFrame, 
        #即末端是包含的  



data.head()  
#返回data的前几行数据，默认为前五行，需要前十行则data.head(10)

data.tail()  
#返回data的后几行数据，默认为后五行，需要后十行则data.tail(10)

data.iloc[-1]   #选取DataFrame最后一行，返回的是Series
data.iloc[-1:]   #选取DataFrame最后一行，返回的是DataFrame

data.loc['a',['w','x']]   #返回‘a’行'w'、'x'列，这种用于选取行索引列索引已知

data.iat[1,1]   #选取第二行第二列，用于已知行、列位置的选取。


```

- 以属性方式访问，对DataFrame是列名，对Series是键。例如`df.A`, `df.A.a`
- `.at`,`.iat`和`.get_value`，获取单个值，注意两者的区别。df.at[‘a’,‘A’], df.get_value(‘a’,‘A’)。他们等价于df.loc[‘a’,‘A’]。这个比采用[]速度要快，遍历的时候推荐用这个。

```python
df = pd.DataFrame([[0, 2, 3], [0, 4, 1], [10, 20, 30]],
                   columns=['A', 'B', 'C'])
print(df)
'''
    A   B   C
0   0   2   3
1   0   4   1
2  10  20  30
'''
print(df.at[2, 'B'])
#20

print(df.at[2, 2])
#ValueError: At based indexing on an non-integer index can only have non-integer indexers

print(df.get_value(2,'B'))
#20

print(df.get_value(2,2))
#只能根据标签索引

```

