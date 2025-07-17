## 🔸 What is NumPy?

NumPy stands for **Numerical Python**.  
It is a Python library used for **working with arrays**.

It also provides functions for:

- Linear algebra
- Fourier transform
- Matrices

NumPy is an **open-source project** and can be used freely.

---

## 🔸 Why Use NumPy?

- It is **much faster** than Python lists.
- Supports **large multi-dimensional arrays** and **matrices**.
- Includes **powerful mathematical functions**.

---

## 🔸 Why NumPy is Faster than Python Lists

## 1. Homogeneous vs Heterogeneous

- A **Python list** can contain mixed data types (e.g., `[1, "a", 3.14]`), so it stores **references (pointers)** to objects.
- **NumPy arrays** store elements of the **same data type**, which allows:
  - Efficient memory usage
  - SIMD (Single Instruction, Multiple Data) operations

## 2. Memory Efficiency

- **Python lists** store pointers to each object, leading to **non-contiguous memory**.
- **NumPy** stores data in a **contiguous memory block**, which the CPU can access more efficiently (better **cache locality**).

## 3. Vectorization – No More Loops!
Vectorization means **applying an operation to an entire array at once**, instead of looping through each element individually.
- NumPy avoids `for` loops by using **vectorized operations**, which are:
  - Faster
  - Cleaner
  - More efficient
- These operations are written in **C** behind the scenes, which makes them much faster than pure Python loops.
- NumPy **uses** **SIMD** (Single Instruction, Multiple Data), meaning:
  - Your **CPU executes the same instruction on multiple data points simultaneously**.

#### 🔸 Simple Analogy
Think of it like:
- **Python loop** → does one operation at a time (slow)
- **NumPy vectorized** → sends one instruction to act on all values at once (fast)
It's like giving one instruction to **4 workers at once**, instead of repeating it **4 times**.

---

## 🔸NumPy Array vs Python List

| Feature           | Python List                              | NumPy Array                                      |
|-------------------|-------------------------------------------|--------------------------------------------------|
| **Type**          | Built-in Python data structure            | Provided by the NumPy library                    |
| **Data Type**     | Can hold mixed data types                 | Homogeneous (all elements must be of same type)  |
| **Performance**   | Slower for numerical operations           | Much faster due to optimized C backend           |
| **Memory Usage**  | Higher                                    | Lower (more compact)                             |
| **Functionality** | Basic operations (append, pop, slice)     | Advanced mathematical operations (e.g., matrix multiplication, broadcasting) |
| **Indexing**      | Basic indexing and slicing                | Advanced indexing, slicing, and broadcasting     |
| **Best For**      | General-purpose programming               | Scientific computing and numerical analysis      |

### 🧪 Example
```python
import numpy as np

# Python list
py_list = [1, 2, 3]
py_list_squared = [x**2 for x in py_list]  # List comprehension

# NumPy array
np_array = np.array([1, 2, 3])
np_array_squared = np_array ** 2  # Vectorized operation
```

- In the list example, you need a loop or list comprehension.
- In the NumPy example, the operation is vectorized, making it cleaner and faster

### ✅ When to Use What?
- Use **Python lists** for general-purpose tasks, especially when working with **mixed data types** or **small datasets**.
- Use **NumPy arrays** when you need **speed**, **efficiency**, and **advanced mathematical operations** on **large numerical datasets**.

---

## 🔸 np.empty()
- np.empty() creates an array without initializing its values.
  It allocates memory for the array but doesn’t set the values to 0 or anything — the contents are just whatever happens to be in memory at that time (random garbage values).
- np.empty() is used when you want an arry but you plan to fill the array later
 ---
 ## 🔸reshape Vs resize
**reshape()**
- Returns a new array or view with the new shape
- Does not modify the original array
- The total number of elements must remain the same
- Memory efficient: Often returns a view (not a copy) when possible
  ```python
  arr = np.array([[1, 2], [3, 4]])
  new_arr = arr.reshape(1, 4)  # Original array unchanged
  print(arr)      # [[1, 2], [3, 4]]
  print(new_arr)  # [[1, 2, 3, 4]]
  ```
**resize()**
- Modifies the array in-place
- Can change the total number of elements
- If new size is larger: array is expanded, new elements filled with zeros
- If new size is smaller: array is truncated
```python
arr = np.array([[1, 2], [3, 4]])
arr.resize(3, 3)  # Original array is modified
print(arr)  
# [[1, 2, 0],
#  [3, 4, 0],
#  [0, 0, 0]]
```
---
## 🔸 flatten Vs ravel()
| Feature              | ravel()                                                                                    | flatten()                                                                         | 
|----------------------|--------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Return type          | Returns only reference/view of the original array                                          | Returns copy of the original array                                                | 
| Modification effect  | If you modify the array you would notice that the value of the original array also changes | If you modify any value of this array value of the original array is not affected | 
| Performance          | Ravel is faster than flatten() as it does not occupy any memory                            | Flatten() is comparatively slower than ravel() as it occupies memory              | 
| Implementation       | Ravel is a library-level function                                                          | Flatten is a method of an ndarray object.                                         | 

```python
import numpy as np

arr = np.array([[1, 2], [3, 4]])

# Using ravel()
raveled = arr.ravel()
raveled[0] = 99  # This will modify the original array too (if view was returned)
print("After modifying raveled:")
print("raveled:", raveled)  # [99  2  3  4]
print("original:", arr)    # [[99  2], [ 3  4]]

# Reset array
arr = np.array([[1, 2], [3, 4]])

# Using flatten()
flattened = arr.flatten()
flattened[0] = 99  # This will NOT modify the original array
print("\nAfter modifying flattened:")
print("flattened:", flattened)  # [99  2  3  4]
print("original:", arr)        # [[1  2], [3  4]]
```
---
## 🔸Can NumPy Store Different Types of Objects in an Array?
Yes, but with limitations. NumPy can store different types of objects in an array using the dtype=object, but this comes with important trade-offs.

Object Arrays in NumPy
```pythin
import numpy as np
# Creating an array with mixed types
mixed_array = np.array([1, 'hello', 3.14, [1, 2, 3], {'key': 'value'}], dtype=object)
print(mixed_array)  # [1 'hello' 3.14 list([1, 2, 3]) {'key': 'value'}]
```
**Limitations and Trade-offs**
Performance   --	Object arrays are much slower than homogeneous arrays  
Memory        --	Less efficient memory usage compared to typed arrays  
Vectorization --	Most NumPy's optimized operations won't work with object arrays  
Storage	      -- Stores references to Python objects, not the actual objects  

---
## 🔸Indexing & Slicling
 **1. Basic Indexing (Like Python Lists)**
✅ 1D Array
```python
import numpy as np
arr = np.array([10, 20, 30, 40])
print(arr[0])  # 10
print(arr[-1]) # 40 (last element)
```
✅ 2D Array
```python
arr2d = np.array([[1, 2, 3],
                  [4, 5, 6]])
print(arr2d[0][1])     # 2
print(arr2d[0, 1])     # 2 (better/faster)
print(arr2d[1, -1])    # 6
```
**2. Slicing (Start:Stop:Step)**
```python
arr = np.array([10, 20, 30, 40, 50])
print(arr[1:4])     # [20 30 40]
print(arr[:3])      # [10 20 30]
print(arr[::2])     # [10 30 50]
```
✅ 2D Slicing
```python
arr2d = np.array([[1, 2, 3],
                  [4, 5, 6],
                  [7, 8, 9]])

print(arr2d[0:2, 1:3])  # [[2 3], [5 6]]
```
**3. Fancy Indexing (Index with List or Array)**
✅ 1D Fancy Indexing
```python
arr = np.array([10, 20, 30, 40, 50])
print(arr[[1, 3, 4]])  # [20 40 50]
```
✅ 2D Fancy Indexing
```python
arr2d = np.array([[1, 2],
                  [3, 4],
                  [5, 6]])
```
Get specific elements using row and col indexes
```python
print(arr2d[[0, 1, 2], [1, 0, 1]])  # [2 3 6]
```
**4. Boolean Indexing (Filter using conditions)**
```python
arr = np.array([10, 15, 20, 25])
print(arr[arr > 15])  # [20 25]
```
✅ Combine with logical operators
```python
print(arr[(arr > 10) & (arr < 25)])  # [15 20]
```
**5. Indexing with np.where()**
```python
arr = np.array([10, 15, 20, 25])
index = np.where(arr > 15)
print(index)         # (array([2, 3]),)
print(arr[index])    # [20 25]
```
---
## 🔸 Array operations
**1. Element-wise Arithmetic**
When you apply +, -, *, or / to two NumPy arrays (or an array and a scalar), it applies the operation to each element individually.
Example:
```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([10, 20, 30])

print(a + b)  # [11 22 33]
print(a - b)  # [-9 -18 -27]
print(a * b)  # [10 40 90]
print(b / a)  # [10. 10. 10.]
```
➡ With Scalar:
```python
print(a + 5)  # [6 7 8]
```
➡ Works element-by-element, no need for loops!

**2. Element-wise Comparison**
Returns a Boolean array showing where the condition is True.
```python
a = np.array([1, 2, 3])

print(a > 2)   # [False False  True]
print(a == 2)  # [False  True False]
print(a != 1)  # [False  True  True]
```
These Boolean arrays are often used in filtering or masking.

**3. Logical Operations**
For combining multiple conditions:
You can’t use and or or with arrays. Use NumPy’s logical functions instead.

np.logical_and() and np.logical_or()
```python
a = np.array([10, 20, 30, 40])

# Select values between 15 and 35
condition = np.logical_and(a > 15, a < 35)
print(condition)      # [False  True  True False]
print(a[condition])   # [20 30]
```
Also works with:
```python
# Same thing using & and | (with parentheses)
print(a[(a > 15) & (a < 35)])  # [20 30]
```
**4. Broadcasting**
Broadcasting allows NumPy to do operations between arrays of different shapes.
Scalar + Array
```python
a = np.array([1, 2, 3])
print(a + 5)  # [6 7 8]
```
2D + 1D (Row or Column)
```python
a = np.array([[1, 2, 3],
              [4, 5, 6]])

b = np.array([10, 20, 30])  # Shape (3,)

print(a + b)
# [[11 22 33]
#  [14 25 36]]
```
➡ b is broadcasted across rows automatically.

**Broadcasting Rules (Simplified)**
- If shapes are equal → element-wise operation.
- If one shape is 1 → it is broadcasted (stretched).
- If shapes can’t be aligned → error.

---






