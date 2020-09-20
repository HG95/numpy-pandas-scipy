# 函数最小值optimize.minimize

因为在生活中，人们总是希望幸福值或其它达到一个极值，比如做生意时希望成本最小，收入最大，所以在很多商业情境中，都会遇到求极值的情况。

`minimize` 求解函数的极小值（无约束）

```python
  scipy.optimize.minimize(fun, x0, 
                          args=(), method=None, 
                          jac=None, hess=None, 
						  hessp=None, bounds=None, 
                          constraints=(), tol=None, 
                          callback=None, options=None)
```

- `fun`：可调用对象，待优化的函数。最开始的参数是待优化的自变量；后面的参数由`args`给出
- `x0`：自变量的初始迭代值
- `args`：一个元组，提供给`fun`的额外的参数
- `method`：一个字符串，指定了最优化算法。可以为：`'Nelder-Mead'`、`'Powell'`、`'CG'`、 `'BFGS'`、`'Newton-CG'`、`'L-BFGS-B'`、`'TNC'`、`'COBYLA'`、`'SLSQP'`、 `'dogleg'`、`'trust-ncg'`
- `jac`：一个可调用对象（最开始的参数是待优化的自变量；后面的参数由`args`给出），雅可比矩阵。只在`CG/BFGS/Newton-CG/L-BFGS-B/TNC/SLSQP/dogleg/trust-ncg`算法中需要。如果`jac`是个布尔值且为`True`，则会假设`fun`会返回梯度；如果是个布尔值且为`False`，则雅可比矩阵会被自动推断（根据数值插值）。
- `hess/hessp`：可调用对象（最开始的参数是待优化的自变量；后面的参数由`args`给出），海森矩阵。只有`Newton-CG/dogleg/trust-ncg`算法中需要。二者只需要给出一个就可以，如果给出了`hess`，则忽略`hessp`。如果二者都未提供，则海森矩阵自动推断
- `bounds`：一个元组的序列，给定了每个自变量的取值范围。如果某个方向不限，则指定为`None`。每个范围都是一个`(min,max)`元组。
- `constrants`：一个字典或者字典的序列，给出了约束条件。只在`COBYLA/SLSQP`中使用。字典的键为：
  - `type`：给出了约束类型。如`'eq'`代表相等；`'ineq'`代表不等
  - `fun`：给出了约束函数
  - `jac`：给出了约束函数的雅可比矩阵（只用于`SLSQP`）
  - `args`：一个序列，给出了传递给`fun`和`jac`的额外的参数
- `tol`：指定收敛阈值
- `options`：一个字典，指定额外的条件。键为：
  - `maxiter`：一个整数，指定最大迭代次数
  - `disp`：一个布尔值。如果为`True`，则打印收敛信息
- `callback`：一个可调用对象，用于在每次迭代之后调用。调用参数为`x_k`，其中`x_k`为当前的参数向量

返回值：返回一个`OptimizeResult`对象。其重要属性为：

- `x`：最优解向量
- `success`：一个布尔值，表示是否优化成功
- `message`：描述了迭代终止的原因



> 因为 `Scipy.optimize.minimize` 提供的是最小化方法，所以最大化距离就相当于最小化距离的负数：在函数的前面添加一个负号

# 基本使用

假设我们要求解最小值的函数为：
$$
f(x, y)=(1-x)^{2}+100\left(y-x^{2}\right)^{2}
$$
则雅可比矩阵为：
$$
\left[\frac{\partial f(x, y)}{\partial x}, \frac{\partial f(x, y)}{\partial y}\right]
$$
则海森矩阵为：
$$
\left[\begin{array}{cc}
\frac{\partial^{2} f(x, y)}{\partial x^{2}} & \frac{\partial^{2} f(x, y)}{\partial x \partial y} \\
\frac{\partial^{2} f(x, y)}{\partial y \partial x} & \frac{\partial^{2} f(x, y)}{\partial y^{2}}
\end{array}\right]
$$
于是有：

```python
  def fun(p):
    x,y=p.tolist()#p 为数组，形状为 (2,)
    return f(x,y)
  def jac(p):
    x,y=p.tolist()#p 为数组，形状为 (2,)
    return np.array([df/dx,df/dy])
  def hess(p):
    x,y=p.tolist()#p 为数组，形状为 (2,)
    return np.array([[ddf/dxx,ddf/dxdy],[ddf/dydx,ddf/dyy]])
```



# 案例 0

计算 $$1/x+x$$ 的最小值

```python
from scipy.optimize import minimize
import numpy as np
 
#demo 1
#计算 1/x+x 的最小值
def fun(x):
    return 1/x + x
 

x0 = np.asarray((2))  # 初始猜测值
res = minimize(fun, x0, method='SLSQP')
print(res)
```

```
# 结果： 
     fun: 2.0000000815356342
     jac: array([0.00057095])
 message: 'Optimization terminated successfully.'
    nfev: 19
     nit: 6
    njev: 6
  status: 0
 success: True
       x: array([1.00028559])
```



# 案例 1

计算函数：
$$
f(x, y)=(1-x)^{2}+100\left(y-x^{2}\right)^{2} 
$$


的最小值

雅可比矩阵为:
$$
\left[400 x\left(x^{2}-y\right)+2(x-1) \quad 200\left(y-x^{2}\right)\right]
$$
海森矩阵为:
$$
\left[\begin{array}{cc}
400\left(3 x^{2}-y\right)+2 & -400 x \\
-400 x & 200
\end{array}\right]
$$

```python
def func(p):
    x, y = p
    return (1-x)**2 + 100*(y-x**2)**2


def jac(p):
    x, y = p
    return np.array([2*(x-1)+400*x*(x**2-y), 200*(y-x**2)])


def hess(p):
    x, y = p
    return np.array([
        [400*(3*x**2-y)+2, -400*x],
        [-400*x, 200]
    ])

result = opt.minimize(func, x0=[10, 10],
                      method='Newton-CG',
                      jac=jac,
                      hess=hess)
result
```

结果：

```
     fun: 1.5507998929041444e-18
     jac: array([ 4.09654832e-07, -2.05662731e-07])
 message: 'Optimization terminated successfully.'
    nfev: 83
    nhev: 51
     nit: 51
    njev: 133
  status: 0
 success: True
       x: array([1., 1.])
```



# 案例 2

计算  $$(2+x1)/(1+x2) - 3*x1+4*x3$$  的最小值  $$x1,x2,x3$$ 的范围都在0.1到0.9 之间

```python
from scipy.optimize import minimize
import numpy as np
 
# demo 2
#计算  (2+x1)/(1+x2) - 3*x1+4*x3 的最小值  x1,x2,x3的范围都在0.1到0.9 之间
def fun(args):
    a,b,c,d=args
    v=lambda x: (a+x[0])/(b+x[1]) -c*x[0]+d*x[2]
    return v
def con(args):
    # 约束条件 分为eq 和ineq
    #eq表示 函数结果等于0 ； ineq 表示 表达式大于等于0  
    x1min, x1max, x2min, x2max,x3min,x3max = args
    cons = ({'type': 'ineq', 'fun': lambda x: x[0] - x1min},\
              {'type': 'ineq', 'fun': lambda x: -x[0] + x1max},\
             {'type': 'ineq', 'fun': lambda x: x[1] - x2min},\
                {'type': 'ineq', 'fun': lambda x: -x[1] + x2max},\
            {'type': 'ineq', 'fun': lambda x: x[2] - x3min},\
             {'type': 'ineq', 'fun': lambda x: -x[2] + x3max})
    return cons


#定义常量值
args = (2,1,3,4)  #a,b,c,d
#设置参数范围/约束条件
args1 = (0.1,0.9,0.1, 0.9,0.1,0.9)  #x1min, x1max, x2min, x2max,x3min, x3max
cons = con(args1)
#设置初始猜测值  
x0 = np.asarray((0.5,0.5,0.5))

res = minimize(fun(args), x0, method='SLSQP',constraints=cons)
```

结果：

```
     fun: -0.773684210526435
     jac: array([-2.47368421, -0.80332409,  4.        ])
 message: 'Optimization terminated successfully.'
    nfev: 10
     nit: 2
    njev: 2
  status: 0
 success: True
       x: array([0.9, 0.9, 0.1])
```



# 参考

- <a href="http://www.huaxiaozhuan.com/工具/scipy/chapters/scipy.html" target="_blank">huaxiaozhuan: Scipy</a> 
- <a href="https://blog.csdn.net/sinat_17697111/article/details/81534935" target="_blank">python 非线性规划（scipy.optimize.minimize）</a> 
- <a href="http://lijin-thu.github.io/04. scipy/04.05 minimization in python.html#minimize-函数" target="_blank">最小化函数:minimize 函数</a> 
- <a href="https://www.cnblogs.com/NaughtyBaby/p/5590081.html" target="_blank">幻大米：最优化</a>