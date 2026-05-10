# Spiral Matrix Traversal

## Concept Overview

Spiral Matrix Traversal is a matrix traversal technique where elements are visited layer by layer in a spiral pattern.

The traversal order is:

- Left → Right
- Top → Bottom
- Right → Left
- Bottom → Top

After completing one layer, the boundaries are updated, and the process repeats for the inner layer.

## Example:

```
1 → 2 → 3
        ↓
4 → 5   6
↑       ↓
7 ← 8 ← 9
```

## Output:

`[1,2,3,6,9,8,7,4,5]`

## Key Idea
We maintain four boundaries:
- **top**    -> starting row
- **bottom** -> ending row
- **left**   -> starting column
- **right**  -> ending column
These boundaries shrink after completing each traversal direction.

## Boundary Initialization
type definitions for matrix dimensions:
```c++
int m = matrix.size();
int n = matrix[0].size();
```
Initial boundary values:
```c++
int top = 0;
int bottom = m - 1;
int left = 0;
int right = n - 1;
```

# Traversal Directions

## 1. Left to Right
- Row remains constant
- Column changes
- We traverse the top row:

```cpp
for (int i = left; i <= right; i++) {
    ans.push_back(matrix[top][i]);
}
```
- Then, increment `top`:

```cpp
top++;
```
- *After traversal:*
  - Because the top row has already been processed.

---

## 2. Top to Bottom
- Column remains constant
- Row changes
- We traverse the right column:

```cpp
for (int i = top; i <= bottom; i++) {
    ans.push_back(matrix[i][right]);
}
```
- Then, decrement `right`:

```cpp
right--;
```
- *After traversal:*
  - Because the right column has already been processed.

---

## 3. Right to Left
- Row remains constant
- Column changes
- We traverse the bottom row:

```cpp
dfor (int i = right; i >= left; i--) {
    ans.push_back(matrix[bottom][i]);
}
```
- Then, decrement `bottom`:

```cpp
bottom--;
```
- *After traversal:*
  - Because the bottom row has already been processed.


# 4. Bottom to Top

- Column remains constant
- Row changes
- We traverse the left column:

```cpp
for (int i = bottom; i >= top; i--) {
    ans.push_back(matrix[i][left]);
}
```
- After traversal, increment `left`:

```cpp
left++;
```

**Because the left column has already been processed, we update `left` after traversal.**

## Why Boundary Updates Are Important

- If boundaries are not updated properly:
  - Corner elements may overlap.
  - Some elements may be printed multiple times.
- Boundary shrinking ensures:
  - Every element is visited exactly once.
  - Traversal moves toward the inner layer correctly.

# Important Conditions

## Before performing:
- Right → Left traversal
- Bottom → Top traversal

We must check whether boundaries are still valid.

```cpp
if (top <= bottom) && (left <= right)
```

These checks prevent duplicate traversal in matrices with:
- Single row
- Single column
- Odd dimensions


# Complete Code

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {

        int m = matrix.size();
        int n = matrix[0].size();

        int top = 0;
        int bottom = m - 1;

        int left = 0;
        int right = n - 1;

        vector<int> ans;

        while (left <= right && top <= bottom) {

            // Left to Right
            // Row is constant -> top
            for (int i = left; i <= right; i++) {
                ans.push_back(matrix[top][i]);
            }
            top++;

            // Top to Bottom
            // Column is constant -> right
            for (int i = top; i <= bottom; i++) {
                ans.push_back(matrix[i][right]);
            }
            right--;

            // Right to Left
            // Row is constant -> bottom
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    ans.push_back(matrix[bottom][i]);
                }
                bottom--;
            }

            // Bottom to Top
            // Column is constant -> left
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    ans.push_back(matrix[i][left]);
                }
                left++;
            }
        }

        return ans;
    }
p};
```


# Time Complexity
- **O(m × n)**
- Every element is visited exactly once.

# Space Complexity
- **O(1)**
- Ignoring the output array.

# Common Mistakes
1. **Forgetting Boundary Checks**
   
   Wrong:
   ```c++
   for (int i = right; i >= left; i--)
   ```
   
   without:
   ```c++
   if (top <= bottom)
   ```
   
   This may duplicate elements.
2. **Updating Boundaries Too Early**

   Incorrect boundary updates can skip elements or revisit elements.

   Always update boundaries after finishing a traversal direction.
3. **Confusing Row and Column Movement**

### Remember:
| Direction | Constant | Changing |
| --- | --- | --- |
| Left → Right | Row | Column |
| Top → Bottom | Column | Row |
| Right → Left | Row | Column |
| Bottom → Top | Column | Row |

# Key Takeaways
- Spiral traversal is controlled using four boundaries.
- Boundaries shrink after each directional traversal.
- Validity checks prevent duplicate traversal.
- Understanding which dimension changes is the key to solving matrix traversal problems correctly.
- Each matrix layer is processed independently from outer to inner.

            
            
            
