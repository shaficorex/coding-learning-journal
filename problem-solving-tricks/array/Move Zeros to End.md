# 📌 Move Zeros to End (In-Place)

## Concept Overview

Given an integer array, the task is to move all 0s to the end while maintaining the relative order of non-zero elements. The operation must be performed in-place without using extra space for another array.

## Key Principles
- Maintain the relative order of non-zero elements (stable operation).
- Modify the original array (in-place).
- Optimize for O(n) time complexity.
- Prefer O(1) auxiliary space.

## Approach 1: Brute Force

### Idea
- Create a new array and store all non-zero elements.
- Count how many zeros are left.
- Append those zeros at the end.
- Copy the result back to the original array.

### Code
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        vector<int> v;

        // Step 1: store non-zero elements
        for (int ele : nums) {
            if (ele != 0) v.push_back(ele);
        }

        // Step 2: append zeros
        int remaining = nums.size() - v.size();
        for (int i = 0; i < remaining; i++) {
            v.push_back(0);
        }

        // Step 3: copy back to original array
        for (int i = 0; i < nums.size(); i++) {
            nums[i] = v[i];
        }
    }
};
```

# Approach 2: Optimal (Two Pointer Technique)

## Idea
- Find the first index `j` where `nums[j] == 0`.
- Traverse from `j+1` using pointer `i`.
- When a non-zero element is found at `i`, swap it with `j`.
- Move `j` forward to the next zero position.

## Step-by-Step Logic
1. Initialize `j = -1`.
2. Find the first zero index and assign it to `j`.
3. If no zero exists, return (array already valid).
4. Traverse from `j + 1`:
   - If `nums[i] != 0`,
     - Swap `nums[i]` and `nums[j]`
     - Increment `j`

## Code
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int j = -1;

        // Step 1: find first zero
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] == 0) {
                j = i;
                break;
            }
        }

        // Step 2: if no zero found, do nothing
        if (j == -1) return;

        // Step 3: move non-zero elements forward
        for (int i = j + 1; i < nums.size(); i++) {
            if (nums[i] != 0) {
                swap(nums[i], nums[j]);
                j++;
            }
        }
    }
};
```

## Important Notes / Edge Cases
- If the array has no zeros, no operation is needed.
- If all elements are zeros, array remains unchanged.
- Works correctly for:
  - Single element arrays
  - Already sorted arrays
  - Mixed positive/negative values


## Complexity
- **Time:** O(n)
- **Space:** O(n)


# Common Mistakes
- Using extra space when the problem requires in-place.
- Not maintaining the order of non-zero elements.
- Forgetting to move pointer `j` after swapping.
- Starting `j` incorrectly without finding the first zero.

# Key Takeaways
- This is a classic two-pointer problem.
- The optimal solution ensures:
  - Single pass after setup
  - Constant space
- Core idea: maintain a position where the next non-zero should go.
