# Remove Duplicates from Sorted Array (Two Pointer Approach)

## Concept Overview

Given a sorted array in non-decreasing order, remove duplicates in-place such that each unique element appears only once. Return the count of unique elements `k`, with the first `k` positions of the array containing the result.

## Key Principles
- The array is already sorted, so duplicates are adjacent.
- Use two pointers to avoid extra space.
- Perform operations in-place (`O(1)`) extra space.

## Explanation

Since the array is sorted, any duplicate elements will be next to each other. This allows a linear scan to identify and overwrite duplicates.

- Maintain a pointer `i` for the position of the last unique element.
- Traverse the array using another pointer `j`.
- When a new unique element is found (`nums[j] != nums[i]`), place it at `i + 1` and move `i`.

## Code Example
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;

        int i = 0; // pointer for last unique element

        for (int j = 1; j < nums.size(); j++) {
            if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];
            }
        }

        return i + 1;
    }
};
```

# Step-by-Step Logic

- Assume the first element is always unique → initialize `i = 0`.
- Start scanning from the second element (`j = 1`).
- Compare `nums[j]` with `nums[i]`:
  - If equal → skip (duplicate).
  - If different → increment `i` and copy `nums[j]` to `nums[i]`.
- After the loop, indices `0` → `i` contain all unique elements.
- Return `i + 1` as the count of unique elements.

## Important Notes / Edge Cases

- If the array is empty, return 0.
- Works only because the array is sorted.
- The elements beyond index `k - 1` are irrelevant.

## Common Mistakes

- Starting `j` from 0 instead of 1.
- Forgetting to increment `i` before assignment.
- Using extra space (e.g., set) when not required.
- Trying this approach on an unsorted array without sorting first.

## Time and Space Complexity

- **Time:** O(n)
- **Space:** O(1)


# Vector Element Deletion (C++ Reference)

## Delete by Index
```cpp
v.erase(v.begin() + index);
```

## Delete a Range
```cpp
v.erase(v.begin() + start, v.begin() + end);
```

## Delete by Value (Remove-Erase Idiom)
```cpp
v.erase(remove(v.begin(), v.end(), value), v.end());
```

## Delete Last Element
```cpp
v.pop_back();
```

## Clear Entire Vector
```cpp
v.clear();
```

## Key Takeaways
- Sorted property enables efficient duplicate removal.
- Two-pointer technique is optimal for in-place modification.
- No need for extra data structures.
- Understanding pointer movement is critical for correctness.
