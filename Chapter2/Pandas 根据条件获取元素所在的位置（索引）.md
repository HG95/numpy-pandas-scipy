# Pandas 根据条件获取元素所在的位置（索引） 



# `.index.tolist()`

在 dataframe 中根据一定的条件，得到符合要求的某行元素所在的位置。

```python
df = pd.DataFrame({'BoolCol': [1, 2, 3, 3, 4],
                   'attr': [22, 33, 22, 44, 66]
                  },
       			  index=[10,20,30,40,50]
                 )
print(df)

'''

	BoolCol	attr
10	1	22
20	2	33
30	3	22
40	3	44
50	4	66
'''
a = df[(df.BoolCol==3)&(df.attr==22)].index.tolist()
print(a)

```

选取“BoolCol”取值为3且“attr”取值为22的行，得到该行在df中的位置

```python
a = df[(df.BoolCol==3)&(df.attr==22)].index.tolist()
# a=30
```

```python
df.BoolCol==3
10    False
20    False
30     True
40     True
50    False
Name: BoolCol, dtype: bool
```

```python
_temp = {'job':['farmer', 'teacher', 'worker', 'acter', 'present'], 'money':[3000, 7000, 5000, 100000, 66666]}
df = pd.DataFrame(_temp)
print(df)
>>        job   money
>>0   farmer    3000
>>1  teacher    7000
>>2   worker    5000
>>3    acter  100000
>>4  present   66666
a = df[(df['money']>10000)].index.tolist()
print(a)
>>[3, 4]



```

