# Pandas drop函数

删除表中的某一行或者某一列更明智的方法是使用drop，它不改变原有的df中的数据，而是返回另一个dataframe来存放删除后的数据。

## **清理无效数据**

```python
df[df.isnull()]  #返回的是个true或false的Series对象（掩码对象），进而筛选出我们需要的特定数据。
df[df.notnull()]

df.dropna()     #将所有含有nan项的row删除
df.dropna(axis=1,thresh=3)  #将在列的方向上三个为NaN的项删除
df.dropna(how='ALL')        #将全部项都是nan的row删除
```

## **drop函数的使用**

### 删除行、删除列

```python
print frame.drop(['a'])
print frame.drop(['Ohio'], axis = 1)
```

**drop 函数默认删除行，列需要加`axis = 1` **

### `inplace`参数 

```python
1. DF= DF.drop('column_name', axis=1)；
2. DF.drop('column_name',axis=1, inplace=True)
3. DF.drop([DF.columns[[0,1, 3]]], axis=1, inplace=True)   # Note: zero indexed
```

注意：凡是会对原数组作出修改并返回一个新数组的，往往都有一个 inplace可选参数。如果手动设定为True（默认为False），那么原数组直接就被替换。也就是说，采用 inplace=True 之后，原数组名（如2和3情况所示）对应的内存值直接改变；

而采用 inplace=False 之后，原数组名对应的内存值并不改变，需要将新的结果赋给一个新的数组或者覆盖原数组的内存位置（如1情况所示）。

### 数据类型转换

```python
df['Name'] = df['Name'].astype(np.datetime64)
```

`DataFrame.astype() `方法可对整个 DataFrame 或某一列进行数据格式转换，支持 Python 和 NumPy 的数据类型。