# 📌 Find Missing Number (0 to n Range)

## Concept Overview

Given an array of size `n` containing **distinct numbers** in the range `[0, n]`, **exactly one number is missing**. The goal is to find that missing number efficiently.

## Key Principles
- The array contains `n` distinct elements.
- The values range from `0` to `n` (inclusive) → total `n + 1` possible numbers.
- Exactly one number is missing.

## Efficient Solutions Should Aim For:
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

## Explanation

Instead of using extra space (like a frequency array), we can use a mathematical approach:

👉 The sum of numbers from `0` to `n` is:

```math
t(n) = \frac{n(n+1)}{2}
```

Compute the expected sum using this formula.
Compute the actual sum of the given array.
The difference between them gives the missing number.

## Code Example (C++)
```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();  // since one number is missing
        
        int expectedSum = n * (n + 1) / 2;
        
        int actualSum = 0;
        for (int num : nums) {
            actualSum += num;
        }
        
        return expectedSum - actualSum;
    }
};
```

# Step-by-Step Logic

- Let `n = nums.size()`
- Calculate expected sum → `n * (n + 1) / 2`
- Calculate actual sum by iterating through array

## Subtract:

`missing = expectedSum - actualSum`

# Important Notes / Edge Cases

- Works even if 0 is missing.
- Works if `n` itself is missing.
- No need to sort the array.
- No need for extra memory.

# Common Mistakes

- Using incorrect formula like `n*(n-1)/2` ❌
- Misinterpreting `n`:
  - `n` is array size, not the maximum number.
- Overflow (rare case):
  - For very large `n`, consider using `long long`.

# Key Takeaways

- Convert a search problem into a math problem.
- Eliminates need for extra space.
- Clean and optimal solution: O(n) time, O(1) space.
- Frequently asked in coding interviews.
