# Traversing Column by Column in Matrix

## Normally matrix access is:

```cpp
matrix[row][col]
```

Meaning:

- `matrix[i][j]`
  - where:
    - `i` = row index
    - `j` = column index

## Row-wise Traversal

Most common traversal:

```cpp
for(int i = 0; i < rows; i++) {
    for(int j = 0; j < cols; j++) {
        cout << matrix[i][j] << " ";
    }
}
```

### Traversal order:

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |
| 7 | 8 | 9 |

### Output:

`1 2 3 4 5 6 7 8 9`

*Because rows are fixed first.*

# Column-wise Traversal

To traverse column by column:

- Outer loop = columns
- Inner loop = rows

```cpp
for(int col = 0; col < cols; col++) {
    for(int row = 0; row < rows; row++) {
        cout << matrix[row][col] << " ";
    }
}
```

## Important Mental Model

Even during column traversal:

`matrix[row][col]`

**NEVER** changes.

Only loop order changes.

## Example

### Matrix:

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |
| 7 | 8 | 9 |

### Column-wise traversal:
- **Column 0:**
  - 1
  - 4
-7
- 
- **Column 1:**
-2
-5
-8
- **Column 2:**
-3
-6
-9

### Final order:
`1 4 7 2 5 8 3 6 9`


# Common Beginner Mistake
People write:
`matrix[col][row]`
**WRONG.**
Because the first index is **ALWAYS** the row.
Correct:
`matrix[row][col]`

---

## Easy Rule to Remember
If traversing:

- **Row-wise:** outer loop iterates over rows
- **Column-wise:** outer loop iterates over columns

> **BUT access always:**
> `matrix[row][col]`

---

## Generic Template
### Row-wise traversal
```cpp
dfor(int row = 0; row < rows; row++) {
    for(int col = 0; col < cols; col++) {
        // your code here
    }
}
```

### Column-wise traversal
```cpp
dfor(int col = 0; col < cols; col++) {
    for(int row = 0; row < rows; row++) {
        // your code here
    }
}
```
