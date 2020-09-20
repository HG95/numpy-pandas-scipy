# cum累积计算函数 

cum系列函数是作为DataFrame或Series对象的方法出现的，因此命令格式为D.cumsum()

|  方法名   |             函数功能              |
| :-------: | :-------------------------------: |
| cumsum()  |   依次给出前1、2、… 、n个数的和   |
| cumprod() |   依次给出前1、2、… 、n个数的积   |
| cummax()  | 依次给出前1、2、… 、n个数的最大值 |
| cummin()  | 依次给出前1、2、… 、n个数的最小值 |

```python
D=pd.Series(range(0,20))
D.cumsum() 
0       0
1       1
2       3
3       6
....
19    190
dtype: int64
```

