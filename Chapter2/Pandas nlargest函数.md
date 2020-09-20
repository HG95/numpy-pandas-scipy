# Pandas nlargest函数

## `nlargest()`

```python
DataFrame.nlargest(self, n, columns, keep='first') → 'DataFrame'
```

返回按列降序排列的前`n`行。

以降序返回`column`中具有最大值的前`n`行。未指定的列也将返回，但不用于排序。

此方法等效于 ，但性能更高。`df.sort_values(columns, ascending=False).head(n)`

参数

- `n` : `int`要返回的行数。

- **columns** ：标签或标签列表要排序的列标签。

- **keep** ：`{'first'，'last'，'all'}`，默认为`'first'`其中有重复的值:
  - 1) **first**：优先处理第一次出现的事件
  - 2) **last**：确定最后出现的优先顺序
  - 3) **all**: 请勿丢弃任何重复项，即使这意味着选择n个以上的项目。

## pandas的分组取最大多行

选择不同location_road下的前五名要怎么操作呢？

很多人可能第一反应会想到先分组然后进行max()操作，但是这样的操作只能选择最大的一列：

<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200514112135.png"/> 





## `nsmallest()` 

用法相同

参考

<a href="https://www.jianshu.com/p/312c4586346d" blank="">pandas的分组取最大多行并求和函数</a> 

