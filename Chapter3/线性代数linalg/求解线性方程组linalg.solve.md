# 求解线性方程组linalg.solve

`numpy`中的求解线性方程组：`numpy.linalg.solve(a, b)`。而`scipy`中的求解线性方程组：

```python
scipy.linalg.solve(a, b, 
                   sym_pos=False, 
                   lower=False, 
                   overwrite_a=False,   
                   overwrite_b=False, 
                   debug=False, 
                   check_finite=True)
```

- `a`：方阵，形状为 `(M,M)`
- `b`：一维向量，形状为`(M,)`。它求解的是线性方程组 。如果有  个线性方程组要求解，且 `a`，相同，则 `b`的形状为 `(M,k)`
- `sym_pos`：一个布尔值，指定`a`是否正定的对称矩阵
- `lower`：一个布尔值。如果`sym_pos=True`时：如果为`lower=True`，则使用`a`的下三角矩阵。默认使用`a`的上三角矩阵。
- `overwrite_a`：一个布尔值，指定是否将结果写到`a`的存储区。
- `overwrite_b`：一个布尔值，指定是否将结果写到`b`的存储区。
- `check_finite`：如果为`True`，则检测输入中是否有`nan`或者`inf`

返回线性方程组的解。

通常求解矩阵 $$A^{-1}B$$，如果使用`solve(A,B)`，要比先求逆矩阵、再矩阵相乘来的快。

# 普通使用

求解线性方程组：
$$
\left[\begin{array}{ccc}
1 & 2 & 3 \\
4 & 9 & 1 \\
27 & 1 & 8
\end{array}\right] \mathbf{x}=\left[\begin{array}{c}
1 \\
1 \\
1
\end{array}\right]
$$

```python
import numpy as np
from scipy.linalg import solve

a = np.array([[1,2,3],
            [4,9,1],
            [27,1,8]])

b = np.array([1,1,1])

x = solve(a,b)
x
```

结果：

```
array([-0.05030488,  0.10213415,  0.2820122 ])
```

