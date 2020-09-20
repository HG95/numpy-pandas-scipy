# 矩阵的LU分解

## linalg.lu

$$M*N$$ 矩阵 $$A$$ 的 `LU` 分解为：
$$
A =PLU
$$
P 是 M×M 的单位矩阵的一个排列，L 是下三角阵，U 是上三角阵。

可以使用 `linalg.lu` 进行 LU 分解的求解：

具体原理可以查看维基百科： https://en.wikipedia.org/wiki/LU_decomposition

```python
A = np.array([[1,2,3],[4,5,6]])

P, L, U = linalg.lu(A)
```

结果：

```
# p
array([[0., 1.],
       [1., 0.]])
       
# L
array([[1.  , 0.  ],
       [0.25, 1.  ]])
       
# U
array([[4.  , 5.  , 6.  ],
       [0.  , 0.75, 1.5 ]])
```






## scipy.linalg.lu_factor

```python
scipy.linalg.lu_factor(a, 
                       overwrite_a=False, 
                       check_finite=True)
```

- `a`：方阵，形状为`(M,M)`，要求非奇异矩阵
- `overwrite_a`：一个布尔值，指定是否将结果写到`a`的存储区。
- `check_finite`：如果为`True`，则检测输入中是否有`nan`或者`inf`

返回:

- `lu`：一个数组，形状为`(N,N)`，该矩阵的上三角矩阵就是`U`，下三角矩阵就是`L`（`L`矩阵的对角线元素并未存储，因为它们全部是1）
- `piv`：一个数组，形状为`(N,)`。它给出了`P`矩阵：矩阵`a`的第 `i`行被交换到了第`piv[i]`行



矩阵`LU`分解：
$$
A=PLU
$$
其中： $$P$$为转置矩阵，该矩阵任意一行只有一个1，其他全零；任意一列只有一个1，其他全零。$$L$$ 为单位下三角矩阵（对角线元素为1）， $$U$$为上三角矩阵（对角线元素为0）

## 基本使用

矩阵 $$LU$$ 分解
$$
\left[\begin{array}{ccc}
1 & 2 & 3 \\
4 & 9 & 1 \\
27 & 1 & 8
\end{array}\right]
$$


```python
import numpy as np
from scipy.linalg import lu_factor

a = np.array([[1,2,3],[4,9,1],[27,1,8]])
lu,piv=lu_factor(a)
```

结果：

```
# lu
array([[27.        ,  1.        ,  8.        ],
       [ 0.14814815,  8.85185185, -0.18518519],
       [ 0.03703704,  0.22175732,  2.74476987]])
```

$$L$$ 为单位下三角矩阵（对角线元素为1）， $$U$$为上三角矩阵

也可使使用上面的`  linalg.lu` 求出 $$L,U$$ 

