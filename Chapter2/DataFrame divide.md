# DataFrame divide

```python
DataFrame.divide(other, axis='columns', level=None, fill_value=None)
```

Get Floating division of dataframe 

Equivalent to `dataframe / other`, but with support to substitute a fill_value for missing data in one of the inputs.

Among flexible wrappers (add, sub, mul, div, mod, pow) to arithmetic operators: +, -, *, /, //, %, **.

Parameters : 

- **other** : **scalar, sequence, Series, or DataFrame**

- **axis** : **{0 or ‘index’, 1 or ‘columns’}**

  Whether to compare by the index (0 or ‘index’) or columns (1 or ‘columns’). For Series input, axis to match Series index on.

- **fill_value** :  **float or None, default None**

  Fill existing missing (NaN) values, and any new element needed for successful DataFrame alignment, with this value before computation. If data in both corresponding DataFrame locations is missing the result will be missing.

返回值 ： **DataFrame**

```python
final
```

<img src=".\img\image-20200905152942510.png" alt="image-20200905152942510" style="zoom:80%;" />

```python
result = final.divide(final['当月新增'],axis = 0).iloc[:,1:]
result['当月新增'] = final['当月新增']
result
```

<img src=".\img\image-20200905153046985.png" alt="image-20200905153046985" style="zoom:80%;" />

```python
final.divide([10, 100, 1000, 10000, 100000], axis=0).iloc[:, 1:]
```

<img src=".\img\image-20200905153810940.png" alt="image-20200905153810940" style="zoom:80%;" />