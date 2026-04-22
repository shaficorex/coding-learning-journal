# 📘 Left Rotate Array by K Places

## 🔹 Concept Overview

Left rotation of an array means shifting each element to the left by *k* positions. Elements that move past the beginning wrap around to the end.

## 🔹 Key Principles
- Rotation depends on array size `n`
- Effective rotation is `k % n` (since rotating `n` times results in the same array)
- Two main approaches:
  - **Extra space (Brute Force)**
  - **In-place (Optimal using reversal)**

## 🔹 Explanation

Given:

```plaintext
nums = [3, 4, 1, 5, 3, -5], k = 8
```

and 

```plaintext
n = 6
```

the effective rotation is calculated as:

```plaintext
y = k % n = 8 % 6 = 2
```

So we rotate the array **2 steps left**:

```plaintext
[3, 4, 1, 5, 3, -5] → [1, 5, 3, -5, 3, 4]
```

# 🧪 Approach 1: Brute Force (Using Extra Space)

## 🔹 Idea
- Store first `d = k % n` elements in a temporary array
- Shift remaining elements to the left
- Place stored elements at the end

## 🔹 Code
```cpp
class Solution {
public:
    void rotateArray(vector<int>& nums, int k) {
        int n = nums.size();
        int d = k % n;

        vector<int> temp;

        // Step 1: Store first d elements
        for (int i = 0; i < d; i++) {
            temp.push_back(nums[i]);
        }

        // Step 2: Shift remaining elements
        for (int i = d; i < n; i++) {
            nums[i - d] = nums[i];
        }

        // Step 3: Put temp elements at the end
        for (int i = n - d; i < n; i++) {
            nums[i] = temp[i - (n - d)];
        }
    }
};
```

## 🔹 Complexity
- **Time:** O(n)
- **Space:** O(n)


# ⚡ Approach 2: Optimal (Reversal Algorithm)

## 🔹 Idea

Instead of extra space, use reversal:

For left rotation by `d`:

1. Reverse first `d` elements
2. Reverse remaining `n - d` elements
3. Reverse entire array

## 🔹 Code
```cpp
class Solution {
public:
    void rotateArray(vector<int>& nums, int k) {
        int n = nums.size();
        int d = k % n;

        reverse(nums.begin(), nums.begin() + d);
        reverse(nums.begin() + d, nums.end());
        reverse(nums.begin(), nums.end());
    }
};
```

## 🔹 Step-by-Step Example

For `nums = [3, 4, 1, 5, 3, -5]`, `d = 2`:

- Reverse first 2 → `[4, 3, 1, 5, 3, -5]`
- Reverse rest → `[4, 3, -5, 3, 5, 1]`
- Reverse whole → `[1, 5, 3, -5, 3, 4]`


# Complexity
- **Time:** O(n)
- **Space:** O(1) (in-place)

## ⚠️ Important Notes / Edge Cases
- Always compute `k % n` to avoid unnecessary rotations.
- Handle edge cases when:
  - `n == 0` (avoid division by zero)
  - `k == 0` (no change)
- Works for negative values in array as well (no special handling needed).

## ❌ Common Mistakes
- Forgetting `k % n`
- Wrong index calculation when copying back temp array
- Confusing left rotation with right rotation
- Incorrect reversal order in optimal approach

## ✅ Key Takeaways
- Left rotation shifts elements and wraps around.
- `k % n` is an essential optimization.
- Brute force is intuitive but uses extra space.
- Reversal algorithm is the most efficient solution (in-place).
- This pattern is commonly asked in coding interviews.
