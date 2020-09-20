# Pandas map, applymap and apply的区别

## **apply()**

<a href="[https://hg1227.github.io/numpy-pandas-scipy/Chapter2/Pandas%20Apply%E5%87%BD%E6%95%B0.html#pandas-apply%E5%87%BD%E6%95%B0](https://hg1227.github.io/numpy-pandas-scipy/Chapter2/Pandas Apply函数.html#pandas-apply函数)" blank=""> Pandas Apply函数</a>

pandas 的 `apply()` 函数可以作用于 `Series` 或者整个 `DataFrame`，功能也是自动遍历整个 `Series` 或者 `DataFrame`, 对每一个元素运行指定的函数。

```python
In [116]: frame = DataFrame(np.random.randn(4, 3), 
                            columns=list('bde'), 
                            index=['Utah', 'Ohio', 'Texas', 'Oregon'])

In [117]: frame
Out[117]: 
               b         d         e
Utah   -0.029638  1.081563  1.280300
Ohio    0.647747  0.831136 -1.549481
Texas   0.513416 -0.884417  0.195343
Oregon -0.485454 -0.477388 -0.309548

In [118]: f = lambda x: x.max() - x.min()

In [119]: frame.apply(f)
Out[119]: 
b    1.133201
d    1.965980
e    2.829781
dtype: float64
```

## **applymap()**

如果想让方程作用于DataFrame中的每一个元素，可以使用`applymap()`

```python
In [120]: format = lambda x: '%.2f' % x

In [121]: frame.applymap(format)
Out[121]: 
            b      d      e
Utah    -0.03   1.08   1.28
Ohio     0.65   0.83  -1.55
Texas    0.51  -0.88   0.20
Oregon  -0.49  -0.48  -0.31
```

## **map()**

`map()`只要是作用将函数作用于一个Series的每一个元素，用法如下所示

```python
In [122]: frame['e'].map(format)
Out[122]: 
Utah       1.28
Ohio      -1.55
Texas      0.20
Oregon    -0.31
Name: e, dtype: object
```

总的来说就是`apply()`是一种让函数作用于列或者行操作，`applymap()`是一种让函数作用于DataFrame每一个元素的操作，而`map`是一种让函数作用于Series每一个元素的操作

`map` 也可以用字典进行映射

```python
data = pd.read_csv("data.csv")

data['gender'].head()
```

结果：

```
0    1.0
1    0.0
2    2.0
3    1.0
4    2.0
Name: gender, dtype: float64
```

```python
mp = {
    0:'未知',
    1:'男',
    2:'女'    
}

data['gender'] = data['gender'].map(mp)

data['gender'].head()
```

结果：

```
0     男
1    未知
2     女
3     男
4     女
Name: gender, dtype: object
```

key 或者 value 必须有一个是 int 型的值

```python
company_size_map = {
    "2000人以上": 6,
    "500-2000人": 5,
    "150-500人": 4,
    "50-150人": 3,
    "15-50人": 2,
    "少于15人": 1
}
workYear_map = {
    "5-10年": 5,
    "3-5年": 4,
    "1-3年": 3,
    "1年以下": 2,
    "应届毕业生": 1
}
```

```python
df["company_size"] = df["companySize"].map(company_size_map)
df["work_year"] = df["workYear"].map(workYear_map)
```



参考

<a href="https://blog.csdn.net/u010814042/article/details/76401133" blank="">Pandas 中map, applymap and apply的区别</a> 