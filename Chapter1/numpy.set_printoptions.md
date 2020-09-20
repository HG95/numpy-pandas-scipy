# numpy.set_printoptions()

`set_printoptions()` 设置输出样式 

```python
numpy.set_printoptions(precision=None, 
						threshold=None, 
						edgeitems=None, 
						linewidth=None, 
						suppress=None, 
						nanstr=None, 
						infstr=None, 
						formatter=None
				)[source]

```

- `precision `: int, optional，float输出的精度，即小数点后维数，默认8（ Number of digits of precision for floating point output (default 8)）

- `threshold` : int, optional，当数组数目过大时，设置显示几个数字，其余用省略号（Total number of array elements which trigger summarization rather than full repr (default 1000).）

- `edgeitems `: int, optional，边缘数目（Number of array items in summary at beginning and end of each dimension (default 3)）.

- `linewidth`  : int, optional，The number of characters per line for the purpose of inserting line breaks (default 75).

- `suppress ` : bool, optional，是否压缩由科学计数法表示的浮点数（Whether or not suppress printing of small floating point values using scientific notation (default False).）

- `nanstr `: str, optional，String representation of floating point not-a-number (default nan).

- `infstr` : str, optional，String representation of floating point infinity (default inf).



**浮点精度可设置：**

```python
>>> np.set_printoptions(precision=4)
>>> print(np.array([1.123456789]))
[ 1.1235]

```

**长数组可概括为：**

```python
>>> np.set_printoptions(threshold=5)
>>> print(np.arange(10))
[0 1 2 ..., 7 8 9]

```

`np.set_printoptions(threshold=np.nan)`
**设置打印时显示方式, `threshold=np.nan` 意思是输出数组的时候完全输出，不需要省略号将中间数据省略**





参考：

<http://doc.codingdict.com/NumPy_v111/reference/generated/numpy.set_printoptions.html#numpy.set_printoptions>

