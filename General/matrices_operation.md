# 🔸 Matrix Addition
✅ Both matrices must have the same dimensions — same number of rows and same number of columns.
Example:
```python
A =  [ [1, 2],
       [3, 4] ]

B =  [ [5, 6],
       [7, 8] ]
```
Both are 2×2 matrices → ✅ We can add them.

--- 

🔸 How Do You Add Them?
You simply add each corresponding element.
```python
A + B = [ [1+5, 2+6],
          [3+7, 4+8] ]

      = [ [6, 8],
          [10, 12] ]
```

---

🔸 General Formula
If
A = [aᵢⱼ] and B = [bᵢⱼ],
then
A + B = [aᵢⱼ + bᵢⱼ]

Where i = row number, and j = column number.

---

🔸 Python Example Using NumPy
```python
import numpy as np

A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

result = A + B
print(result)
```
Output:
```python
[[ 6  8]
 [10 12]]
```

---

🔸 Key Points to Remember
Rule / Concept	Explanation
Same size required	Number of rows and columns must match
Element-wise addition	Add each pair of corresponding elements
Result is same shape	The result will be the same dimension as the input matrices

---

# 🔸 Matrix Multiplication
For two matrices A (of size m×n) and B (of size n×p):
✅ Matrix multiplication is possible only when the number of columns of A = number of rows of B.
A = m×n
B = n×p
Result = m×p

✅ Example
```python
A = [ [1, 2],
      [3, 4] ]     → 2×2 matrix

B = [ [5, 6],
      [7, 8] ]     → 2×2 matrix

we multiply row by row
[1×5 + 2×7,  1×6 + 2×8] → [19, 22]
[3×5 + 4×7,  3×6 + 4×8] → [43, 50]

A × B = [ [19, 22],
          [43, 50] ]
```

---

🔸 General Formula
If:
A is an m×n matrix
B is an n×p matrix
Then element at position (i, j) in result is:
result[i][j] = sum(A[i][k] * B[k][j] for k in range(n))

---

🔸 Python Code Using NumPy
```python
import numpy as np

A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

result = np.dot(A, B)
print(result)
```
Output:
```python
[[19 22]
 [43 50]]
```
You can also use A @ B instead of np.dot(A, B).

---

🔸 Important Notes
Rule / Concept	Explanation
Matrix multiplication ≠ element-wise	It's a row-by-column operation
Inner dimensions must match	Columns of A = Rows of B
Resulting shape	m×p (rows of A × columns of B)

---
