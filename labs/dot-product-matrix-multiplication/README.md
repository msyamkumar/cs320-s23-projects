# Vector Dot Product and Matrix Multiplication

In lecture, we've talked about what the dot product means to multiply
a vector by a vector.  Here, we'll review that, and also learn what it
means to multiply a matrix by a vector, or a matrix by a matrix.

### 1. Dot Product of Two Vectors

Complete the following function so that it compute the dot product of
two vectors:

```python
def v_v_dot_product(v1, v2):
    assert len(v1) == len(v2)
    total = 0
    for i in range(len(v1)):
        total += ????
    return total

a = np.array([100,10,1])
b = np.array([3,2,0])
v_v_dot_product(a, b) # should be 320
```

<details>
    <summary>ANSWER</summary>
    <code>v1[i] * v2[i]</code>
</details>

### 2. Matrix - Vector Multiplication

We can multiply a matrix by a vector by doing vector-by-vector
multiplications, taking one row at a time from the matrix for the
first vector.  This will give us a vector containing output value per
row in the matrix.

Complete the following function so that it computes the multiplication of
a matrix and a 1-dimensional vector (vertical):

```python
def m_v_multiplication(m, v):
    output = []
    for row in m:
        assert len(row) == len(v)
        output.append(????)
    return np.array(output)

A = np.array([
    [1,0,3],
    [0,2,3],
])
x = np.array([1,10,100])
m_v_multiplication(A, x) # should be [301, 320]
```

<details>
    <summary>ANSWER</summary>
    <code>v_v_dot_product(row, v)</code>
</details>

### 3. Matrix - Matrix Multiplication

We can multiply a matrix by a matrix by doing matrix-by-vector
multiplications, taking one column at a time from the second matrix
for the vector.  Each of these multiplications gives an output vector
-- arranging these output vectors as columns in an output matrix gives
the result of the matrix multiplication.

Complete the following function so that it compute the multiplication of
a two matrices:

```python
def m_m_multiplication(m1, m2):
    output_cols = []
    for col in m2.T:
        output_cols.append(????)
    return np.array(output_cols).T

A = np.array([
    [1,0],
    [1,2],
    [1,3],
    [0,5],
    [100,200],
])
B = np.array([
    [1,0,10],
    [0,1,1],
])
m_m_multiplication(A, B)
```

The result should be this:

```
array([[   1,    0,   10],
       [   1,    2,   12],
       [   1,    3,   13],
       [   0,    5,    5],
       [ 100,  200, 1200]])
```

<details>
    <summary>ANSWER</summary>
    <code>m_v_multiplication(m1, col)</code>
</details>
