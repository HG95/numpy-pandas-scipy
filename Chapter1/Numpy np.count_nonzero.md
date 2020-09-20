# Numpy np.count_nonzero

```python
numpy.count_nonzero(a)
```

计算数组`a`中非零值的数量。

| 参数： | **a**：array_like要为其计数非零的数组。   |
| :----- | ----------------------------------------- |
| 返回： | **count**：int或数组int数组中的非零值数。 |



```python
>>> np.count_nonzero(np.eye(4))
4
>>> np.count_nonzero([[0,1,7,0,0],[3,0,0,2,19]])
5
```

