# Matrix Transpose

## Concept Overview

Matrix transpose means converting all rows into columns and all columns into rows.

If a matrix is:

- `m × n` before transpose
- it becomes `n × m` after transpose

For a matrix `matrix[i][j]`, the transposed position becomes:

```plaintext
transpose[j][i] = matrix[i][j]
```

### Example:

**Original matrix (2 × 3):**

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |

**After transpose (3 × 2):**

| 1 | 4 |
|---|---|
| 2 | 5 |
| 3 | 6 |

## Key Principle

During transpose:
- Row index becomes column index
- Column index becomes row index

So:
```plaintext
tans[j][i] = matrix[i][j];
```

## Transpose of an m × n Matrix

### Why In-Place Transpose Is Not Possible?
For a non-square matrix (`m × n` where `m != n`):
- The dimensions change after transpose.
- Original matrix size and transposed matrix size are different.

**Example:**
- `2 × 3` → `3 × 2`
- `4 × 2` → `2 × 4`

Because the shape changes, we cannot rearrange elements safely inside the same matrix memory layout.
So, we create a new matrix.


# Approach

Create an answer matrix with size:

```cpp
vector<vector<int>> ans(n, vector<int>(m));
```

Then place elements like this:

```cpp
ans[j][i] = matrix[i][j];
```

## Code Example

```cpp
vector<vector<int>> transpose(vector<vector<int>>& matrix) {
    
    int m = matrix.size();
    int n = matrix[0].size();

    vector<vector<int>> ans(n, vector<int>(m));

    for(int i = 0; i < m; i++) {
        for(int j = 0; j < n; j++) {
            ans[j][i] = matrix[i][j];
        }
    }

    return ans;
}
```

## Step-by-Step Logic

Given:

|  |  |  |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

### Iteration Flow
| `matrix[i][j]` | Goes To |
|-----------------|---------|
| `matrix[0][0] = 1` | `ans[0][0]` |
| `matrix[0][1] = 2` | `ans[1][0]` |
| `matrix[0][2] = 3` | `ans[2][0]` |
| `matrix[1][0] = 4` | `ans[0][1]` |
| `matrix[1][1] = 5` | `ans[1][1]` |
| `matrix[1][2] = 6` | `ans[2][1]` |

# Final matrix

| 1 | 4 |
|---|---|
| 2 | 5 |
| 3 | 6 |



# In-Place Transpose for n × n Matrix

## Why It Works

For a square matrix:

- Number of rows = number of columns
- Matrix size remains the same after transpose

### Example:

`3 × 3 → 3 × 3`

So we can swap elements directly without creating another matrix.

## Important Observation

During transpose:

`matrix[i][j] ↔ matrix[j][i]`

We only swap elements above the diagonal.

### Why?

Because:
- Diagonal elements stay unchanged
- Swapping both sides again would undo the transpose

# In-Place Transpose Code

```cpp
for(int i = 0; i < matrix.size() - 1; i++) {
    for(int j = i + 1; j < matrix.size(); j++) {
        swap(matrix[i][j], matrix[j][i]);
    }
}
```

## Step-by-Step Visualization

### Original matrix:

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |
| 7 | 8 | 9 |

### Swaps:
- swap(2,4)
- swap(3,7)
- swap(6,8)

### Final matrix:

| 1 | 4 | 7 |
|---|---|---|
| 2 | 5 | 8 |
| 3 | 6 | 9 |

## Time Complexity

### Using Extra Matrix:
- **Time Complexity:** O(m × n)
- **Space Complexity:** O(m × n)

### In-Place Square Matrix Transpose:
- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

## Important Notes
1. **Square Matrix Only for In-Place**
   
This approach works only when:
- `rows == columns`

Otherwise, dimensions change after transpose.



## 2. Do Not Swap Entire Matrix

This is wrong:

```cpp
for(int i = 0; i < n; i++)
{
    for(int j = 0; j < n; j++)
    {
        swap(matrix[i][j], matrix[j][i]);
    }
}
```

Because elements get swapped twice and the matrix becomes unchanged again.

## 3. Start j From i + 1

Correct:

```cpp
for(int j = i + 1; j < n; j++)
```

This ensures:
- Diagonal elements are skipped
- Duplicate swaps are avoided

## Common Mistakes
### Mistake 1
Writing:

```cpp
ans[i][j] = matrix[j][i];
```
Correct:

```cpp
ans[j][i] = matrix[i][j];
```


# Mistake 2

Trying in-place transpose for rectangular matrices.

**Example:**

`2 × 3 → 3 × 2`

Dimensions change, so direct swapping is not valid.

# Mistake 3

Swapping lower triangle and upper triangle both.

This causes double swapping.

# Key Takeaways
- Transpose converts rows into columns.
- For transpose:
  ```
  transpose[j][i] = matrix[i][j];
  ```
- `m × n` matrices require an extra matrix.
- `n × n` matrices can be transposed in-place.
- In-place transpose swaps only upper triangle elements.
- Start inner loop from `j = i + 1` to avoid duplicate swaps.
