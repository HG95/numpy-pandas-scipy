# Numpy 数学函数

## 一元的数学函数

- `abs/fabs`：计算整数、浮点数或者复数的绝对值。对于非复数值，可以使用更快的`fabs`
- `sqrt` ：计算平方根，相当于`a**0.5`
- `square`：计算平方，相当于`a**2`
- `exp`：计算指数 
- `log/log10/log2/log1p`：分别为 
- `sign`：计算 
- `ceil`：计算各元素的`ceiling`值：大于等于该值的最小整数
- `floor`：计算个元素的`floor`值：小于等于该值的最大整数
- `rint`：将各元素四舍五入到最接近的整数，保留`dtype`
- `modf`：将数组的小数和整数部分以两个独立数组的形式返回
- `isnan`：返回一个布尔数组，该数组指示那些是`NaN`
- `isfinite/isinf`：返回一个布尔数组，该数组指示哪些是有限的/无限数
- `cos/cosh/sin/sinh/tan/tanh`：普通和双曲型三角函数
- `arccos/arcsosh/arcsin/arcsinh/arctan/arctanh`:反三角函数

