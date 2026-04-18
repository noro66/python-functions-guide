# 3️⃣ Matrix Operations

---

## ✅ Reverse Matrix

```python
def reverse_matrix(matrix):
    new_matrix = []
    for row in matrix:
        new_matrix.append(row[::-1])
    return new_matrix
```

---

## ✅ Transpose Matrix

```python
def transpose_matrix(matrix):
    rows = len(matrix)
    cols = len(matrix[0])
    result = []

    for c in range(cols):
        new_row = []
        for r in range(rows):
            new_row.append(matrix[r][c])
        result.append(new_row)

    return result
```
