# 矩阵的奇异值分解svd

矩阵的奇异值分解： 设矩阵 $$A$$ 为 阶的矩阵，则存在一个分解，使得：$$\mathbf{A}=\mathbf{U} \mathbf{\Sigma} \mathbf{V}^{T}$$ ，其中$$U$$ 为 $$M*M$$ 阶酉矩阵； $$\Sigma$$为半正定的 阶的对焦矩阵； 而$$V$$ 为$$N*N$$ 阶酉矩阵。

 $$\Sigma$$ 对角线上的元素为 $$A$$ 的奇异值，通常按照从大到小排列。

```python
scipy.linalg.svd(a, 
                 full_matrices=True, 
                 compute_uv=True, 
                 overwrite_a=False,  
                 check_finite=True, 
                 lapack_driver='gesdd')
```

- `a`：一个矩阵，形状为`(M,N)`，待分解的矩阵。
- `full_matrices`：如果为`True`，则 $$U$$ 的形状为`(M,M)`、  $$\mathbf{V}^{T}$$ 的形状为`(N,N)`；否则 $$\mathbf{U}$$ 的形状为`(M,K)`、 $$\mathbf{V}^{T}$$ 的形状为`(K,N)`，其中 `K=min(M,N)`
- `compute_uv`：如果`True`，则结果中额外返回`U`以及`Vh`；否则只返回奇异值
- `overwrite_a`：一个布尔值，指定是否将结果写到`a`的存储区。
- `overwrite_b`：一个布尔值，指定是否将结果写到`b`的存储区。
- `check_finite`：如果为`True`，则检测输入中是否有`nan`或者`inf`
- `lapack_driver`：一个字符串，指定求解算法。可以为：`'gesdd'/'gesvd'`。默认的`'gesdd'`。

返回值：

- `U`：  $$U$$矩阵
- `s`：奇异值，它是一个一维数组，按照降序排列。长度为 `K=min(M,N)`
- `Vh`：就是 $$\mathbf{V}^{T}$$ 矩阵



# 基本使用

奇异值分解;
$$
\left[\begin{array}{cccc}
0 & 1 \\
1 & 1 \\
1 & 0
\end{array}\right]
$$

```python
from scipy.linalg import svd

a = np.array([
    [0,1],
    [1,1],
    [1,0]
])
u,s,vt = svd(a)
```

结果：

```python
# u
array([[-0.40824829,  0.70710678,  0.57735027],
       [-0.81649658,  0.        , -0.57735027],
       [-0.40824829, -0.70710678,  0.57735027]])
       
# s
array([1.73205081, 1.        ])

# vt
array([[-0.70710678, -0.70710678],
       [-0.70710678,  0.70710678]])
```





# 参考

- <a href="https://hg1227.github.io/2019/12/18/奇异值分解SVD/#7-python-代码" target="_blank">奇异值分解(SVD)原理与在降维中的应用</a> 
- <a href="https://zhuanlan.zhihu.com/p/26306568" target="_blank">奇异值分解的揭秘（一）：矩阵的奇异值分解过程</a> 

