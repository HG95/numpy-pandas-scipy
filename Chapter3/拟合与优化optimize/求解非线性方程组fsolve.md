# 求解非线性方程组fsolve

使用 `scipy.optimize` 模块的 `fsolve`函数进行数值求解线性及非线性方程，可以看到这一个问题实际上还是一个优化问题，也可以用之前拟合函数的 `leastsq` 求解。下面用这两个方法进行对比：

# scipy.optimize.fsolve

```python
  scipy.optimize.fsolve(func, 
                        x0, args=(), 
                        fprime=None, full_output=0, col_deriv=0,
  						xtol=1.49012e-08, maxfev=0, 
                        band=None, epsfcn=None, 
                        factor=100, diag=None)
```

参数：


- `func`：是个可调用对象，它代表了非线性方程组。给他传入方程组的各个参数，它返回各个方程残差（残差为零则表示找到了根）
- `x0`：预设的方程的根的初始值
- `args`：一个元组，用于给`func`提供额外的参数。
- `fprime`：用于计算`func`的雅可比矩阵（按行排列）。默认情况下，算法自动推算
- `full_output`：如果为`True`，则给出更详细的输出
- `col_deriv`：如果为`True`，则计算雅可比矩阵更快（按列求导）
- `xtol`：指定算法收敛的阈值。当误差小于该阈值时，算法停止迭代
- `maxfev`：设定算法迭代的最大次数。如果为零，则为 `100*(N+1)`，`N`为`x0`的长度
- `band`：If set to a two-sequence containing the number of sub- and super-diagonals within the band of the Jacobi matrix, the Jacobi matrix is considered banded (only for fprime=None)
- `epsfcn`：采用前向差分算法求解雅可比矩阵时的步长。
- `factor`：它决定了初始的步长
- `diag`：它给出了每个变量的缩放因子

返回值：

- `x`：方程组的根组成的数组
- `infodict`：给出了可选的输出。它是个字典，其中的键有：
  - `nfev`：`func`调用次数
  - `njev`：雅可比函数调用的次数
  - `fvec`：最终的`func`输出
  - `fjac`：the orthogonal matrix, q, produced by the QR factorization of the final approximate Jacobian matrix, stored column wise
  - `r`：upper triangular matrix produced by QR factorization of the same matrix
- `ier`：一个整数标记。如果为 1，则表示根求解成功
- `mesg`：一个字符串。如果根未找到，则它给出详细信息



如果要求解方程：

$$
\left\{\begin{array}{l}
f 1(u 1, u 2, u 3)=0 \\
f 2(u 1, u 2, u 3)=0 \\
f 3(u 1, u 2, u 3)=0
\end{array}\right.
$$
那么 func 这么定义：

```python
def func(x):
    u1, u2, u3 = x
    return [f1(u1,u2,u3),f2(u1,u2,u3),f3(u1,u2,u3)]
```

**案例1：**

```python
import scipy.optimize as opt
import numpy as np


def f(x):
    x0, x1, x2 = x
    return np.array([
        5*x1+3,
        4*x0*x0-2*np.sin(x1*x2),
        x1*x2-1.5
    ])


result = opt.fsolve(f, [1, 1, 1])
print("解：",result)
print("各向量的值：",f(result))
```

结果：

```python
解： [-0.70622057 -0.6        -2.5       ]
各向量的值： [ 0.00000000e+00 -9.12603326e-14  5.32907052e-15]
```



同样可以用最小二乘法 `leastsq` 求解上述问题

```python
#拟合函数来求解
h = opt.leastsq(f,[1, 1, 1])
print("解：",h[0])
print("各向量的值：",f(h[0]))
```

结果：

```
解： [-0.70622057 -0.6        -2.5       ]
各向量的值： [ 0.00000000e+00 -2.22044605e-16  0.00000000e+00]
```





**案例2：**

如果给了Jacobian矩阵，那么迭代速度更快
Jacobian矩阵的定义是：
$$
\left[\begin{array}{ccc}
\frac{\partial f 1}{\partial u 1} & \frac{\partial f 1}{\partial u 2} & \frac{\partial f 1}{\partial u 2} \\
\frac{\partial f 2}{\partial u 1} & \frac{\partial f 2}{\partial u 2} & \frac{\partial f 2}{\partial u 2} \\
\frac{\partial f 3}{\partial u 1} & \frac{\partial f 3}{\partial u 2} & \frac{\partial f 3}{\partial u 2}
\end{array}\right]
$$


```python
import scipy.optimize as opt
import numpy as np
def obj_func(x):
    x0,x1,x2=x
    return [5*x1+3,4*x0*x0-2*np.sin(x1*x2),x1*x2-1.5]

def jacobian(x):
    x0, x1, x2 = x
    return [
        [0,5,0],
        [8*x0,-2*x2*np.cos(x1*x2),-2*x1*np.cos(x1*x2)],
        [0,x2,x1]
    ]
result=opt.fsolve(obj_func,[1,1,1],fprime=jacobian)
print("解：",result)
print("各向量的值：",obj_func(result))
```

结果：

```
解： [-0.70622057 -0.6        -2.5       ]
各向量的值： [0.0, -9.126033262418787e-14, 5.329070518200751e-15]
```









# 参考

- <a href="https://blog.csdn.net/guofei9987/article/details/75050307" target="_blank">【解方程】scipy.optimize.solve.</a>
- <a href="https://blog.csdn.net/u011702002/article/details/78078010" target="_blank">python用fsolve、leastsq对非线性方程组进行求解</a> 