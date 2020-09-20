# Pandas 数据对齐输出

用pandas展示数据输出时列名不能对齐 

列名用了中文的缘故，设置pandas的参数即可，代码如下：

```python
import pandas as pd
#这两个参数的默认设置都是False
pd.set_option('display.unicode.ambiguous_as_wide', True)
pd.set_option('display.unicode.east_asian_width', True)


```

