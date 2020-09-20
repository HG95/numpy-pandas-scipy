# 全局最优点basinhopping

常规的最优化算法很容易陷入局部极值点。`basinhopping`算法是一个寻找全局最优点的算法。

```python
scipy.optimize.basinhopping(func, 
                            x0, niter=100, 
                            T=1.0, stepsize=0.5,   
                            minimizer_kwargs=None,
                            take_step=None, 
                            accept_test=None, 
                            callback=None,   
                            interval=50, 
                            disp=False, 
                            niter_success=None)
```

- `func`：可调用函数。为待优化的目标函数。最开始的参数是待优化的自变量；后面的参数由`minimizer_kwargs`字典给出
- `x0`：一个向量，设定迭代的初始值
- `niter`：一个整数，指定迭代次数
- `T`：一个浮点数，设定了“温度”参数。
- `stepsize`：一个浮点数，指定了步长
- `minimizer_kwargs`：一个字典，给出了传递给`scipy.optimize.minimize`的额外的关键字参数。
- `take_step`：一个可调用对象，给出了游走策略
- `accept_step`：一个可调用对象，用于判断是否接受这一步
- `callback`：一个可调用对象，每当有一个极值点找到时，被调用
- `interval`：一个整数，指定`stepsize`被更新的频率
- `disp`：一个布尔值，如果为`True`，则打印状态信息
- `niter_success`：一个整数。Stop the run if the global minimum candidate remains the same for this number of iterations.

返回值：一个`OptimizeResult`对象。其重要属性为：

- `x`：最优解向量
- `success`：一个布尔值，表示是否优化成功
- `message`：描述了迭代终止的原因



# 基本使用

假设我们要求解最小值的函数为：
$$
f(x, y)=(1-x)^{2}+100\left(y-x^{2}\right)^{2}
$$
于是有：

```python
  def fun(p):
    x,y=p.tolist()#p 为数组，形状为 (2,)
    return f(x,y)
```



# 案例 1

求解函数:
$$
f(x, y)=(1-x)^{2}+100\left(y-x^{2}\right)^{2}
$$
的最小值。

```python
import numpy as np
from scipy import optimize as opt

def func(p):
    x, y = p
    return (1-x)**2 + 100*(y-x**2)**2

result = opt.basinhopping(func,x0=np.array([10,10]))
result
```

结果：

```
                        fun: 6.098906415928738e-13
 lowest_optimization_result:       fun: 6.098906415928738e-13
 hess_inv: array([[0.50162481, 1.0026807 ],
       [1.0026807 , 2.00930225]])
      jac: array([ 2.91012054e-05, -1.05691264e-05])
  message: 'Desired error not necessarily achieved due to precision loss.'
     nfev: 444
      nit: 16
     njev: 108
   status: 2
  success: False
        x: array([0.9999995 , 0.99999895])
                    message: ['requested number of basinhopping iterations completed successfully']
      minimization_failures: 30
                       nfev: 17153
                        nit: 100
                       njev: 4199
                          x: array([0.9999995 , 0.99999895])
```



# 参考

- <a href="http://lijin-thu.github.io/" target="_blank">中文 Python 笔记</a> 
- <a href="http://www.huaxiaozhuan.com/工具/scipy/chapters/scipy.html" target="_blank">huaxiaozhuan: Scipy</a> 