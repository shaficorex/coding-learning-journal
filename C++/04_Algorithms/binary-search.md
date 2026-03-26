# Binary Search

## Concept Overview

Binary Search is an efficient algorithm used to find a target value in a **sorted array** by repeatedly dividing the search space in half.

Instead of checking every element (like linear search), it eliminates half of the remaining elements at each step.

**Time Complexity:** O(log n)

---

## Key Principles

- Works **only on sorted arrays** (ascending or descending).
- Maintains two pointers:
  - `left` (start index)
  - `right` (end index)
- Calculates the middle index:
  ```cpp
  mid = left + (right - left) / 2;
  ```

  # Explanation

Start with the full range of the array.
Find the middle element.
Compare it with the target:
- If equal → return index
- If target is smaller → search left half
- If target is larger → search right half
Repeat until the element is found or the range becomes invalid.

## Code Example (C++)
```cpp
int binarySearch(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        }
        else if (nums[mid] > target) {
            right = mid - 1;
        }
        else {
            left = mid + 1;
        }
    }

    return -1; // target not found
}
```

## Step-by-Step Logic
- **Initialize:**
  - `left = 0`
  - `right = n - 1`
- **Loop condition:**
  - `while (left <= right)`
- **Inside loop:**
  - Calculate `mid`
  - Compare `nums[mid]` with `target`
  - Narrow the search space:
    - Left half → `right = mid - 1`
    - Right half → `left = mid + 1`


# Important Notes / Edge Cases

## 1. Sorted Array Requirement

Binary search only works correctly if the array is sorted.

## 2. Loop Invariant (Ascending Order)

During execution:
- All elements before `left` are `< target`
- All elements after `right` are `> target`

## 3. When Loop Ends

Loop stops when:
- `left > right`

At that moment:
- `right` → last index where value `< target`
- `left` → first index where value `≥ target`

👉 This makes **left** the correct insertion position.

## 4. Insert Position Variant
```cpp
int searchInsert(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) return mid;
        else if (nums[mid] > target) right = mid - 1;
        else left = mid + 1;
    }

    return left;
}
```

# Common Mistakes

- Using binary search on an unsorted array
- Infinite loop due to wrong condition (`left < right` instead of `<=`)
- Incorrect updates:
  - Using `right = mid` instead of `mid - 1`
  - Using `left = mid` instead of `mid + 1`

## Integer Overflow in:
```java
mid = (left + right) / 2;
```

# Key Takeaways

- Binary search reduces search space by half each step.
- Requires a sorted array.
- `left <= right` is the correct loop condition.
- After the loop, `left` gives the insertion position.

## Always use:
```java
mid = left + (right - left) / 2;
```
