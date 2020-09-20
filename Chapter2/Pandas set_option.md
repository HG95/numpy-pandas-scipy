# Pandas set_option

```python
pandas.set_option(pat, value) = <pandas._config.config.CallableDynamicDoc object>
```

设置指定选项的值。

`set_option`需要两个参数，并将该值设置为指定的参数值，如下所示：

参数

- **display.max_categories** ：**int**

  This sets the maximum number of categories pandas should output when printing out a Categorical or a Series of dtype “category”. [default: 8] [currently: 8]

- **display.max_columns** ：**int** 

  显示的最大列数

- **display.max_rows** ：**int**

  显示的最大行数

- **display.min_rows** ：**int** 

- **display.precision** ： **int** 

  Floating point output precision (number of significant digits). This is only a suggestion [default: 6] [currently: 6] 设置十进制数显示的精度

- **display.float_format** ：**callable** 

  设置浮点数显示的格式

  

- **display.max_colwidth**  ：**int or None** 
  显示最大列宽设置

用pandas展示数据输出时列名不能对齐

列名用了中文的缘故，设置pandas的参数即可，代码如下：

```python
import pandas as pd
#这两个参数的默认设置都是False
pd.set_option('display.unicode.ambiguous_as_wide', True)
pd.set_option('display.unicode.east_asian_width', True)

```





```python
pd.set_option("display.max_rows",80)

pd.set_option("display.max_columns",32)


```

设置浮点数显示的精度

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818155029.png" alt="image-20200818155006580" style="zoom:80%;" />

你也可以重置任何一个选项为其默认值：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200818155112.png" alt="image-20200818155107028" style="zoom:80%;" />

对于其它的选项也是类似的使用方法。