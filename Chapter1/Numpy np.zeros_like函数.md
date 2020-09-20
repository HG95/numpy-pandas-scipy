# Numpy np.zeros_like()函数

```python
numpy.zeros_like(a,
				 dtype = None,
                 order ='K',
                 subok = True
                )
```

返回与指定数组具有相同形状和数据类型的数组，并且数组中的值都为0。

参数

- `a` ： array_like
       用 `a`的形状和数据类型，来定义返回数组的属性

- `dtype `： 数据类型，可选

  覆盖结果的数据类型。

  

- `order` 顺序 ： {'C'，'F'，'A'或'K'}，可选
  覆盖结果的内存布局。'C'表示C顺序，'F'表示F顺序，'A'表示如果a是Fortran连续，则表示'F'，否则'C'。“K”表示匹配的布局一个尽可能接近。

- `subok `： bool，可选。

  值为True是使用a的内部数据类型，值为False是使用a数组的数据类型，默认为True