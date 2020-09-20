# Numpy 中的矩阵向量乘法

## 结论：

**元素乘法：`np.multiply(a,b)`**

**矩阵乘法：`np.dot(a,b)` 或 `np.matmul(a,b)` 或 `a.dot(b)`**

**唯独注意：`*`，在 np.array 中重载为元素乘法，在 np.matrix 中重载为矩阵乘法!**

## **对于 `np.array`  对象**

```python
>>> a
array([[1, 2],
       [3, 4]])

```

### **元素乘法 **

**用 `a*b` 或 `np.multiply(a,b)`，**

```python
>>> a * a
array([[ 1,  4],
       [ 9, 16]])

>>> np.multiply(a,a)
array([[ 1,  4],
       [ 9, 16]])

```

### **矩阵乘法**

** 用 `np.dot(a,b)`或 `np.matmul(a,b)` 或 `a.dot(b)`。**

```python
>>> np.dot(a,a)
array([[ 7, 10],
       [15, 22]])

>>> np.matmul(a,a)
array([[ 7, 10],
       [15, 22]])

>>> a.dot(a)
array([[ 7, 10],
       [15, 22]])


```

## 对于 `np.matrix` 对象

```python
>>> A
matrix([[1, 2],
        [3, 4]])

```

### **元素乘法 **

**用 `np.multiply(a,b)`**

```python
>>> np.multiply(A,A)
matrix([[ 1,  4],
        [ 9, 16]])

```

### 矩阵乘法 

**用 `a*b` 或 `np.dot(a,b)` 或 `np.matmul(a,b)`或 `a.dot(b)`。**

```python
>>> A*A
matrix([[ 7, 10],
        [15, 22]])
>>> np.dot(A,A)
matrix([[ 7, 10],
        [15, 22]])
>>> np.matmul(A,A)
matrix([[ 7, 10],
        [15, 22]])
>>> A.dot(A)
matrix([[ 7, 10],
        [15, 22]])


```

