# numpy.nan_to_num

```python
numpy.nan_to_num(x, copy=True, nan=0.0, posinf=None, neginf=None)
```

将NaN替换为零，并用大的有限数（默认行为）或用户使用NaN、posinf和/或neginf关键字定义的数字替换NaN。

Parameters

- **x** :scalar or array_like

  Input data.

- **copy**bool, optional

  Whether to create a copy of *x* (True) or to replace values in-place (False). The in-place operation only occurs if casting to an array does not require a copy. Default is True.

  *New in version 1.13.*

- **nan**: int, float, optional

  Value to be used to fill NaN values. If no value is passed then NaN values will be replaced with 0.0.



- **posinf**: int, float, optional

  Value to be used to fill positive infinity values. If no value is passed then positive infinity values will be replaced with a very large number.

- **neginf**: int, float, optional

  Value to be used to fill negative infinity values. If no value is passed then negative infinity values will be replaced with a very small (or negative) number.

## Examples

```python
np.nan_to_num(np.inf)
1.7976931348623157e+308

np.nan_to_num(-np.inf)
-1.7976931348623157e+308

np.nan_to_num(np.nan)
0.0

x = np.array([np.inf, -np.inf, np.nan, -128, 128])
np.nan_to_num(x)
array([ 1.79769313e+308, -1.79769313e+308,  0.00000000e+000, # may vary
       -1.28000000e+002,  1.28000000e+002])

np.nan_to_num(x, nan=-9999, posinf=33333333, neginf=33333333)
array([ 3.3333333e+07,  3.3333333e+07, -9.9990000e+03, 
       -1.2800000e+02,  1.2800000e+02])

y = np.array([complex(np.inf, np.nan), np.nan, complex(np.nan, np.inf)])
array([  1.79769313e+308,  -1.79769313e+308,   0.00000000e+000, # may vary
     -1.28000000e+002,   1.28000000e+002])

np.nan_to_num(y)
array([  1.79769313e+308 +0.00000000e+000j, # may vary
         0.00000000e+000 +0.00000000e+000j,
         0.00000000e+000 +1.79769313e+308j])
np.nan_to_num(y, nan=111111, posinf=222222)

array([222222.+111111.j, 111111.     +0.j, 111111.+222222.j])
```

