# 最小二乘解lstsq

`lstsq`比`solve`更一般化，它不要求矩阵 $$A$$ 是方阵。 它找到一组解 $$X$$，使得 $$\|\mathbf{b}-\mathbf{A} \mathbf{x}\|$$  最小，我们称得到的结果为最小二乘解。

```python
scipy.linalg.lstsq(a, 
                   b, 
                   cond=None, overwrite_a=False, 
                   overwrite_b=False,  
                   check_finite=True, lapack_driver=None)
```

- `a`：为矩阵，形状为`(M,N)`
- `b`：一维向量，形状为`(M,)`。它求解的是线性方程组 $$\mathbf{A} \mathbf{x}=\mathbf{b}$$  。如果有 $$k$$ 个线性方程组要求解，且 `a`，相同，则 `b`的形状为 `(M,k)`
- `cond`：一个浮点数，去掉最小的一些特征值。当特征值小于`cond * largest_singular_value`时，该特征值认为是零
- `overwrite_a`：一个布尔值，指定是否将结果写到`a`的存储区。
- `overwrite_b`：一个布尔值，指定是否将结果写到`b`的存储区。
- `check_finite`：如果为`True`，则检测输入中是否有`nan`或者`inf`
- `lapack_driver`：一个字符串，指定求解算法。可以为：`'gelsd'/'gelsy'/'gelss'`。默认的`'gelsd'`效果就很好，但是在许多问题上`'gelsy'`效果更好。

返回值：

- `x`：最小二乘解，形状和`b`相同
- `residures`：残差。如果 $$rank(A)$$  大于`N`或者小于`M`，或者使用了`gelsy`，则是个空数组；如果`b`是一维的，则它的形状是`(1,)`；如果`b`是二维的，则形状为`(K,)`
- `rank`：返回矩阵`a`的秩
- `s`：`a`的奇异值。如果使用`gelsy`，则返回`None`



# 基本使用

求解线性方程组
$$
\left[\begin{array}{cccc}
1 & 2 & 3 & 4 \\
4 & 9 & 16 & 1 \\
27 & 64 & 1 & 8
\end{array}\right] \mathbf{x}=\left[\begin{array}{c}
1 \\
1 \\
1
\end{array}\right]
$$

```python
import numpy as np
from scipy.linalg import lstsq

a = np.array([[1, 2, 3, 4], [4, 9, 16, 1], [27, 64, 1, 8]])
b = np.array([1, 1, 1])
lstsq(a, b)
```

结果：

```
(array([ 0.00205847, -0.01287038,  0.0558478 ,  0.21403472]),
 array([], dtype=float64),
 3,
 array([70.75236556, 15.95524212,  3.67872487]))
```

