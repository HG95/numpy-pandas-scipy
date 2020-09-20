# 多维插值interp2d

## interp2d

```python
class scipy.interpolate.interp2d(x, y, z, 
                                 kind='linear', 
                                 copy=True, 
                                 bounds_error=False, 
                                 fill_value=None
                                )
```

参数：

`x`, `y`, `z` :

array_like

If the points lie on a regular grid, *x* can specify the column coordinates and *y* the row coordinates, for example:

```
>>> x = [0,1,2];  y = [0,3]; z = [[1,2,3], [4,5,6]]
```

If *x* and *y* are multi-dimensional, they are flattened before use.

**`kind`**：

**{‘linear’, ‘cubic’, ‘quintic’}, optional**

```python
# 生成数据
import numpy as np
def func(x,y):
    return (x+y)*np.exp(-5*(x**2+y**2))
x,y=np.mgrid[-1:1:8j,-1:1:8j]
z=func(x,y)

# 插值
from scipy import interpolate
func=interpolate.interp2d(x,y,z,kind='cubic')

xnew=np.linspace(-1,1,100)
ynew=np.linspace(-1,1,100)
znew=func(xnew,ynew)#xnew, ynew是一维的，输出znew是二维的
xnew,ynew=np.mgrid[-1:1:100j,-1:1:100j]#统一变成二维，便于下一步画图

# 画图
import mpl_toolkits.mplot3d
import matplotlib.pyplot as plt
ax=plt.subplot(111,projection='3d')
ax.plot_surface(xnew,ynew,znew)
ax.scatter(x,y,z,c='r',marker='^')
plt.show()
```

<center>
<img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200106203704.png"/></center>




## 二维插值 Rbf

**二维径向基函数插值**

```python
# 随机生成点，并计算函数值
import numpy as np
def func(x,y):
    return (x+y)*np.exp(-5*(x**2+y**2))

x=np.random.uniform(low=-1,high=1,size=100)
y=np.random.uniform(low=-1,high=1,size=100)
z=func(x,y)

# 插值
from scipy import  interpolate
func=interpolate.Rbf(x,y,z,function='multiquadric')
xnew,ynew=np.mgrid[-1:1:100j,-1:1:100j]
znew=func(xnew,ynew)#输入输出都是二维

# 画图
import mpl_toolkits.mplot3d
import matplotlib.pyplot as plt
ax=plt.subplot(111,projection='3d')
ax.plot_surface(xnew,ynew,znew)
ax.scatter(x,y,z,c='r',marker='^') 
plt.show()
```

<center>
    <img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200106205824.png"/>
</center>




# 参考

1. <a href="https://www.guofei.site/2017/06/06/scipyinterpolate.html" target="">scipy.interpolate</a> 
2. <a href="http://liao.cpython.org/scipytutorial12/" target="">Scipy Tutorial-一元样条插值</a> 
3. <a href="https://docs.scipy.org/doc/scipy/reference/generated/scipy.interpolate.Rbf.html" target="">scipy.interpolate.Rbf</a> 