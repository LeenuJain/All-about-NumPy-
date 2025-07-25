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

**Step-by-Step Guide to Manually Check Broadcasting Compatibility**
Step 1: Write down the shapes of both arrays
Let’s say:
```python
A.shape = (2, 3, 4)
B.shape = (3, 1)
```
You need to compare the shapes from right to left (trailing dimensions first).

Step 2: Pad the smaller shape with 1s (on the left)
```python
A: (2, 3, 4)
B:     (3, 1)  → pad to → (1, 3, 1)
```
Now both shapes are the same length.

Step 3: Compare dimensions one by one (from right to left)
Rule: For each dimension — it's OK if:
They are equal, OR
One of them is 1 (it can be stretched)

So:
Dim	A	B	Result
- 3	2	1	✅ OK (B will stretch)
- 2	3	3	✅ OK
- 1	4	1	✅ OK (B will stretch)

✅ ✅ ✅ → They can be broadcast together!

---

## 🔸 NumPy Math & Stats Function Summary (1D & 2D)

| Function       | Description                  | 1D Example Code         | Output (1D)     | 2D Example Code                           | Output (2D)                         |
|----------------|------------------------------|-------------------------|------------------|-------------------------------------------|-------------------------------------|
| `np.sum()`     | Sum of all elements          | `np.sum([1, 2, 3])`     | `6`              | `np.sum([[1, 2], [3, 4]])`                | `10` (entire array)                 |
|                |                              |                         |                  | `np.sum(..., axis=0)`                     | `[4 6]` (column-wise)               |
|                |                              |                         |                  | `np.sum(..., axis=1)`                     | `[3 7]` (row-wise)                  |
| `np.mean()`    | Average (mean) value         | `np.mean([1, 2, 3])`    | `2.0`            | `np.mean([[1, 2], [3, 4]])`               | `2.5`                               |
| `np.std()`     | Standard deviation           | `np.std([1, 2, 3])`     | `0.816...`       | `np.std([[1, 2], [3, 4]])`                | `1.118...`                          |
| `np.var()`     | Variance                     | `np.var([1, 2, 3])`     | `0.666...`       | `np.var([[1, 2], [3, 4]])`                | `1.25`                              |
| `np.min()`     | Minimum value                | `np.min([4, 1, 9])`     | `1`              | `np.min([[4, 1], [9, 7]])`                | `1`                                 |
| `np.max()`     | Maximum value                | `np.max([4, 1, 9])`     | `9`              | `np.max([[4, 1], [9, 7]])`                | `9`                                 |
| `np.argmin()`  | Index of min value           | `np.argmin([4, 1, 9])`  | `1`              | `np.argmin([[4, 1], [9, 7]])`             | `1` (flattened index)              |
| `np.argmax()`  | Index of max value           | `np.argmax([4, 1, 9])`  | `2`              | `np.argmax([[4, 1], [9, 7]])`             | `2` (flattened index)              |
| `np.cumsum()`  | Cumulative sum               | `np.cumsum([1, 2, 3])`  | `[1 3 6]`        | `np.cumsum([[1, 2], [3, 4]])`             | `[1 3 6 10]` (flattened)           |
| `np.cumprod()` | Cumulative product           | `np.cumprod([1, 2, 3])` | `[1 2 6]`        | `np.cumprod([[1, 2], [3, 4]])`            | `[1 2 6 24]` (flattened)           |
| `np.exp()`     | Exponential (e^x)            | `np.exp([0, 1])`        | `[1. 2.718...]`  | `np.exp([[0, 1], [2, 3]])`                | `[[1. 2.71] [7.38 20.08]]`          |
| `np.log()`     | Natural log (ln)             | `np.log([1, np.e])`     | `[0. 1.]`        | `np.log([[1, np.e], [np.e**2, np.e**3]])` | `[[0. 1.] [2. 3.]]`                 |
| `np.sqrt()`    | Square root                  | `np.sqrt([1, 4, 9])`    | `[1. 2. 3.]`     | `np.sqrt([[1, 4], [9, 16]])`              | `[[1. 2.] [3. 4.]]`                 |

---

## 🔸Cumulative Sum & Cumulative Product
#### Cumulative Sum
It means adding elements one by one and keeping a running total.
Example:
```python
import numpy as np
a = np.array([1, 2, 3, 4]) 
np.cumsum(a)
```
How it works:
| Step | Element | Running Sum     |
|------|---------|------------------|
| 1    | 1       | 1                |
| 2    | 2       | 1 + 2 = 3        |
| 3    | 3       | 3 + 3 = 6        |
| 4    | 4       | 6 + 4 = 10       |

Result:
```python
array([1, 3, 6, 10])
```
#### Cumulative Product
It means multiplying elements one by one and keeping a running product.
Example:
```python
np.cumprod([1, 2, 3, 4])
```
result
```python
array([1, 2, 6, 24])
```
---
## 🔸Random :
**1.np.random.seed()**  
The np.random.seed() function sets the starting point for NumPy's random number generator. It ensures that **you get the same random numbers every time you run your code**.
If you want repeatable results (especially in testing or debugging), you use a seed.

```python
import numpy as np

np.random.seed(42)
print(np.random.rand(3)) # [0.37454012 0.95071431 0.73199394]
```
Every time you run this, you’ll get exactly same output unless you chnage the see value.

**2.np.random.rand() — Uniform distribution [0, 1)**  
Generates random floats between 0 and 1 (exclusive), from a uniform distribution.
```python
a = np.random.rand()
b = np.random.rand(2,)
c = np.random.rand(2, 3)
print(a)
print(b)
print(c)
```
result
```python
0.8611055075863213
[0.08521139 0.32471667]
[[0.66486494 0.16458129 0.45351088]
 [0.87465708 0.6873813  0.09383688]]
```

**3.np.random.randn() — Standard normal distribution**  
Generates random values from a standard normal distribution (mean = 0, std = 1). Can be negative.
```python
a = np.random.randn(2, 3)
print(a)
```
result : 
```python
[[ 0.4967 -0.1383  0.6476]
 [ 1.5230 -0.2341 -0.2341]]
```

**4.np.random.randint() — Random integers**  
Syntax :
```python
np.random.randint(low, high, size)
```
Generates random integers in [low, high)
Example
```python
np.random.randint(10, 20, size=(2, 3))
```
result
```python
[[13 16 19]
 [11 17 10]]
```

**5.np.random.choice() — Randomly pick from a list**  
Syntax : 
```python
np.random.choice(array, size, replace=True/False)
```
- replace=True	-- Random elements, can repeat
- replace=False	-- Random unique elements only

```python
random = np.random.choice([1, 2, 3, 4, 5], size=3)
random_false = np.random.choice([1, 2, 3, 4, 5], size=3, replace=False)
```
result
```python
[1 1 3] 
[2 4 1]
```

**6.np.random.shuffle() — Shuffle an array in-place**  
- Modifies the array directly
- No return value

```python
arr = np.array([1, 2, 3, 4, 5])
np.random.shuffle(arr)
print(arr) # [4 1 5 3 2]
```

---

## 🔸 concatenate()
np.concatenate() is used to **join two or more arrays along an existing axis** (rows or columns, etc.).
Syntax:
```python
np.concatenate((array1, array2), axis=0)
```
- axis=0 → Join along rows (vertically)
- axis=1 → Join along columns (horizontally) — valid for 2D arrays and higher

**1. 1D Arrays – Axis doesn't matter**
```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.concatenate((a, b))
print(result)
```
**Output**
```python
[1 2 3 4 5 6]
```

**2. 2D Arrays — Join Vertically (axis=0)**
```python
a = np.array([[1, 2],
              [3, 4]])
b = np.array([[5, 6],
              [7, 8]])

result = np.concatenate((a, b), axis=0)
print(result)
```
**output**
```python
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
```

**3. 2D Arrays — Join Horizontally (axis=1)**
```python
result = np.concatenate((a, b), axis=1)
print(result)
```

**Output**
```python
[[1 2 5 6]
 [3 4 7 8]]
```

**⚠️ Important Rules**

| Condition   | Requirement                                 |
|-------------|----------------------------------------------|
| Axis = 0    | All arrays must have the **same number of columns** |
| Axis = 1    | All arrays must have the **same number of rows**    |

> ⚠️ If shapes don’t match appropriately, it throws a `ValueError`.

---

## 🔸 stack() 
np.stack() **joins arrays along a new axis.**
> 🔁 Unlike concatenate, which joins along an existing axis, stack adds a new dimension.

**Syntax**
```python
np.stack((array1, array2), axis=0)
```
- axis=0 → Stacks along a new outer axis (adds one more dimension at the beginning)
- axis=1 → Inserts a new axis in the middle

**1. Stack 1D arrays with axis=0**
```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

result = np.stack((a, b), axis=0)
print(result)
```
**Output**
```python
[[1 2 3]
 [4 5 6]]
```
Shape: (2, 3)
→ Two arrays stacked as rows
   
**2. Stack 1D arrays with axis=1**
```python
result = np.stack((a, b), axis=1)
print(result)
```
**Output**
```python
[[1 4]
 [2 5]
 [3 6]]
```
Shape: (3, 2)
→ Two arrays stacked as columns  
  
**3. Stack 2D arrays with axis=0**
```python
a = np.array([[1, 2],
              [3, 4]])

b = np.array([[5, 6],
              [7, 8]])

result = np.stack((a, b), axis=0)
print(result)
```
**Output**
```python
[[[1 2]
  [3 4]]

 [[5 6]
  [7 8]]]
```
 Shape: (2, 2, 2)
→ New dimension added: we now have a 3D array
  
**4. Stack 2D arrays with axis=1**
```python
import numpy as np

a = np.array([[1, 2],
              [3, 4]])

b = np.array([[5, 6],
              [7, 8]])
result = np.stack((a, b), axis=1)
print(result)
```
**Output**
```python
[[[1 2]
  [5 6]]

 [[3 4]
  [7 8]]]
```
Shape: (2, 2, 2)

#### Related Shortcuts

| Function      | Description                                          |
|---------------|------------------------------------------------------|
| `np.vstack()` | Shortcut for `stack(..., axis=0)` for vertical stacking |
| `np.hstack()` | Shortcut for `concatenate(..., axis=1)`              |
| `np.dstack()` | Stacks along depth (adds a new 3rd axis)             |

---

## 🔸 Splitting Arrays

| Function             | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `np.split()`         | Splits array into equal-sized sub-arrays. All parts must be of equal size. |
| `np.array_split()`   | Splits array into approximately equal parts. Works even if sizes are uneven.|

### Example:

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6])

# Using np.split (must divide evenly)
print(np.split(arr, 3))  
# Output: [array([1, 2]), array([3, 4]), array([5, 6])]

# Using np.array_split (can handle uneven splits)
print(np.array_split(arr, 4))  
# Output: [array([1, 2]), array([3, 4]), array([5]), array([6])]
```

### ⚠️ Important Rule:
- `np.split()` raises a `ValueError` if array can’t be divided evenly.
- `np.array_split()` avoids that by adjusting sub-array sizes.

**Splitting 2D Arrays**
```python
arr2d = np.array([[1, 2, 3, 4],
                  [5, 6, 7, 8]])

# Split columns into 2 parts
np.split(arr2d, 2, axis=1)
```
**Output**
```python
[array([[1, 2],
        [5, 6]]), 

 array([[3, 4],
        [7, 8]])]
```

---

## 🔸 squeeze()

`np.squeeze()` **removes axes of size 1** (i.e., dimensions with length 1) from the shape of an array.

#### Syntax:
```python
np.squeeze(a, axis=None)
```

- `a`: The input array  
- `axis` *(optional)*: Remove only specific axis if it’s of size 1 — otherwise, it raises an error.

#### Why use it?

To:
- Reduce dimensions (e.g., from `(1, 3, 1)` to `(3,)`)
- Make arrays more compact
- Prepare arrays for plotting or computation when an extra dimension isn’t needed


#### Example 1: Remove all dimensions of size 1
```python
import numpy as np

arr = np.array([[[10, 20, 30]]])  # Shape: (1, 1, 3)
print("Original shape:", arr.shape)

squeezed = np.squeeze(arr)
print("Squeezed shape:", squeezed.shape)
print(squeezed)
```

**Output**:
```text
Original shape: (1, 1, 3)
Squeezed shape: (3,)
[10 20 30]
```

#### Example 2: Use `axis` to squeeze a specific dimension
```python
arr = np.array([[[1], [2], [3]]])  # Shape: (1, 3, 1)
print(arr.shape)  # (1, 3, 1)

# Remove only axis 0
result = np.squeeze(arr, axis=0)
print(result.shape)  # (3, 1)

# Remove only axis 2
result = np.squeeze(arr, axis=2)
print(result.shape)  # (1, 3)
```

#### Summary Table

| Input Shape | `np.squeeze()` Result |
|-------------|------------------------|
| (1, 3, 1)   | (3,)                   |
| (3, 1)      | (3,)                   |
| (1, 3, 5)   | (3, 5)                 |
| (3, 5)      | (3, 5)                 |


### ⚠️ Important Rule:
- You can only squeeze **axes that have size = 1**.
- Trying to squeeze a dimension with more than 1 element will raise an error **if `axis` is specified**.

---

## 🔸 expand_dims()

`np.expand_dims()` adds a new axis (dimension) to your array at the specified position.

#### Syntax:
```python
np.expand_dims(arr, axis)
```

#### Why use it?

To reshape arrays so they match another array's dimensions — especially useful for:
- Broadcasting
- Batch processing
- Machine learning

#### Example 1: Expanding a 1D Array

```python
import numpy as np

arr = np.array([1, 2, 3])
print(arr.shape)  # (3,)
```

👉 Add a new axis at position `0` (as a row):
```python
expanded = np.expand_dims(arr, axis=0)
print(expanded.shape)  # (1, 3)
print(expanded)
```
**Output**:
```python
[[1 2 3]]
```

👉 Add a new axis at position `1` (as a column):
```python
expanded = np.expand_dims(arr, axis=1)
print(expanded.shape)  # (3, 1)
print(expanded)
```
**Output**:
```python
[[1]
 [2]
 [3]]
```

#### Example 2: Expanding a 2D Array

```python
arr2d = np.array([[1, 2], [3, 4]])
print(arr2d.shape)  # (2, 2)

# Add a new axis at the beginning → shape becomes (1, 2, 2)
expanded = np.expand_dims(arr2d, axis=0)
print(expanded)
```
**Output**:
```python
[[[1, 2],
  [3, 4]]]
```

#### Summary Table

| Original Shape | `axis=0`    | `axis=1`     | `axis=2`     |
|----------------|-------------|--------------|--------------|
| (3,)           | (1, 3)      | (3, 1)       | ❌ Not valid |
| (2, 2)         | (1, 2, 2)   | (2, 1, 2)    | (2, 2, 1)    |

---  


