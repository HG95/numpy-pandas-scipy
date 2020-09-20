# Pandas sample随机抽样

有时候我们只需要数据集中的一部分，并不需要全部的数据。这个时候我们就要对数据集进行随机的抽样。pandas中自带有抽样的方法。

```python
DataFrame.sample(n=None, 
                 frac=None, 
                 replace=False, 
                 weights=None, 
                 random_state=None, 
                 axis=None)
```

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514102644.png"/>